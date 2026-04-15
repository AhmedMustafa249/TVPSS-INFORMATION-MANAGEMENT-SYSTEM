# TVPSS-MAIN Final Verdict — Implementation Issues

## Frontend Issues

### F-1. Status vocabulary mismatch in crew application result UI
- Major category: Implementation/Frontend
- Secondary lens: Contract/Postcondition; Maintainability/Evolvability
- Source: Codex (confirmed by cross-check)
- Location: `TVPSS-MAIN/resources/js/Pages/5-Students/ResultApply.jsx:123-129,236-270`; `TVPSS-MAIN/app/Http/Controllers/StudentController.php:76-80`; `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php:924-939`
- Problem: The backend writes three status strings — `Permohonan Belum Diproses`, `Approved`, and `Rejected`. The modal logic in `ResultApply.jsx` branches on `Diluluskan` and `Dalam Proses`. Badge rendering and modal behavior operate on different vocabularies, so an approved or pending application can render with the correct badge color but wrong modal title and wrong CTA.
- Evidence:
  - `StudentController::applyCrewSubmit()` stores `Permohonan Belum Diproses`.
  - `SchoolAdminController::approveStudcrew()` stores `Approved`; `rejectStudcrew()` stores `Rejected`.
  - `ResultApply.jsx` badge colors handle `Approved` and `Permohonan Belum Diproses`.
  - `ResultApply.jsx` modal title and print action check `Diluluskan` and `Dalam Proses` — strings never written by the backend.
- Why it matters: Student-facing behavior is wrong on the happy path. The postcondition of the school admin approval action is not correctly observable to the student.
- Severity: Medium
- Recommendation: Define one canonical set of crew-application status constants (e.g., a PHP-backed enum or a shared JS constants file) and consume the same values in `StudentController`, `SchoolAdminController`, and `ResultApply.jsx`.
- Expected benefit: Correct student-facing behavior and less brittle UI branching with a single source of truth.

---

## Backend Issues

### B-1. Authorization is absent as a structural boundary
- Major category: Implementation/Backend
- Secondary lens: Architecture/Boundary; Defensive Programming
- Source: Both Codex and Copilot (confirmed and expanded by cross-check)
- Location: `TVPSS-MAIN/bootstrap/app.php:14-18`; `TVPSS-MAIN/routes/web.php:31-46`; `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php:244-313,918-952`; `TVPSS-MAIN/app/Http/Controllers/PPDAdminController.php:162-205,278-282`
- Problem: The `CheckRole` middleware is commented out in `bootstrap/app.php`. All admin-role route files are loaded inside a single `auth/verified` middleware group with no per-role enforcement. Any authenticated user can reach any admin endpoint. Controller methods then use `findOrFail()` on global IDs without school, district, or state scoping — authorization depends entirely on ad-hoc query habits rather than a stable architectural boundary.
- Critical dependency: The cross-check identified that `CheckRole` redirects to route names such as `superADashControl` that are not defined in any route file. Re-enabling the middleware without first correcting those redirect targets will cause immediate route-resolution failures. The natural remediation path is itself broken.
- Evidence:
  - `routes/web.php` includes `schoolAdminRoutes.php`, `ppdAdminRoutes.php`, `stateAdminRoutes.php`, `superAdminRoutes.php` under one shared auth group.
  - `bootstrap/app.php` has `CheckRole` commented out.
  - `SchoolAdminController::saveFollowUp()`, `getFollowUps()`, `editStudcrew()`, `approveStudcrew()`, `rejectStudcrew()`, `destroy()` all use global `findOrFail($id)`.
  - `PPDAdminController::editEquipment()`, `updateEquipment()`, `saveFollowUp()`, `deleteEquipment()` load equipment by raw ID without district scoping.
  - `CheckRole` redirect targets reference route names not present in any route file.
- Why it matters: Every admin endpoint is structurally accessible to any authenticated user. Cross-role and cross-tenant data access is prevented only by developer discipline, not by any enforced boundary. The fix path has a hidden dependency that must be resolved first.
- Severity: High
- Recommendation: (1) Fix `CheckRole` redirect targets to valid named routes before re-enabling. (2) Apply role middleware or policies per route group. (3) Enforce tenant scoping in all mutating controller actions using query scopes or model policies.
- Expected benefit: Restores the role access model as a real structural boundary, reduces cross-role/cross-school data exposure, and eliminates the dependency on per-method developer discipline.

### B-2. Achievement persistence invariant is broken
- Major category: Implementation/Backend
- Secondary lens: Contract/Invariant; Defensive Programming
- Source: Copilot (missed by Codex; confirmed by cross-check)
- Location: `TVPSS-MAIN/database/migrations/2024_12_27_193450_create_student_achievements_table.php`; `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php` (achievement creation methods); `TVPSS-MAIN/app/Models/StudentAchievement.php`
- Problem: The migration declares `$table->id()` (bigint auto-increment), but the controller assigns string IDs of the form `PS0001`. The same migration declares a foreign key on `student_id` without first defining the `student_id` column. This is a migration that cannot execute correctly in a relational context and a schema whose constraints are never enforced.
- Compounding factor: Because `config/database.php` defaults to MongoDB and models extend the MongoDB Eloquent driver (see B-3), migration "success" on MongoDB gives false confidence. FK constraints are never processed, so the broken schema is invisible until application-level data integrity failures appear.
- Evidence:
  - Migration uses `$table->id()` (bigint auto-increment).
  - `SchoolAdminController` achievement creation assigns `'PS' . str_pad(count, 4, '0', STR_PAD_LEFT)` to `id`.
  - Migration declares `$table->foreign('student_id')` without a prior `$table->unsignedBigInteger('student_id')` or equivalent column definition.
- Why it matters: Data written to achievements will either violate the type contract silently or fail at query time. The FK declaration references a non-existent column. Silent data integrity failures are worse than loud ones because they accumulate undetected.
- Severity: High
- Recommendation: Choose one identity strategy. If domain codes are needed, add an explicit `achievement_code` column alongside a numeric PK. Define the `student_id` column before declaring the FK constraint. Verify migration correctness against both MongoDB and SQL environments.
- Expected benefit: Reliable migrations, stable persistence invariants, and correct cross-model relationships.

### B-3. MongoDB-default + SQL-style migrations create a silent persistence correctness gap
- Major category: Implementation/Backend
- Secondary lens: Architecture/Boundary; Application System Reuse
- Source: Copilot (missed by Codex; confirmed by cross-check)
- Location: `TVPSS-MAIN/config/database.php`; all migration files; all models extending `MongoDB\Laravel\Eloquent\Model`
- Problem: The application defaults to MongoDB. Models extend `MongoDB\Laravel\Eloquent\Model`. Yet migration files throughout the project use `->foreignId()`, `->constrained()`, and `->references()->on()` — SQL relational constructs that MongoDB does not process. No FK constraint is ever enforced at the database layer. Every relational invariant documented in migrations is silently ignored at runtime.
- Evidence:
  - `config/database.php` sets `'default' => 'mongodb'`.
  - Models extend `MongoDB\Laravel\Eloquent\Model`.
  - Migration files use `->foreignId()`, `->constrained()`, and `->references('id')->on('table')`.
- Why it matters: Developers reading migrations believe relational constraints exist and are enforced. The database enforces none of them. This affects correctness analysis of every inter-model relationship in the system. It also means Finding B-2 (achievement schema) is worse than it appears: the broken FK is invisible in normal operation.
- Severity: High
- Recommendation: Commit explicitly to MongoDB and remove all SQL-style FK declarations, replacing them with application-level validation or document-embedding patterns. Alternatively, switch to a SQL database and run relational migrations against it. Do not maintain SQL migration artifacts against a MongoDB backend.
- Expected benefit: Honest schema documentation that reflects what the database actually enforces, and a reliable foundation for future data integrity analysis.

### B-4. Payment integration has hard-coded secrets and a dev-environment URL
- Major category: Implementation/Backend
- Secondary lens: Application System Reuse; Defensive Programming
- Source: Copilot (missed by Codex; confirmed by cross-check)
- Location: `TVPSS-MAIN/app/Http/Controllers/paymentController.php`
- Problem: `userSecretKey`, `categoryCode`, and `https://dev.toyyibpay.com` are literal constants embedded in the controller. There is no adapter interface. Provider swap requires controller surgery. Secret rotation requires a code commit. The dev endpoint URL is in the production code path.
- Evidence:
  - `paymentController.php` contains hard-coded `userSecretKey`, `categoryCode`, and `https://dev.toyyibpay.com`.
- Why it matters: Active security risk (secrets in source), portability failure (dev URL in production path), and zero ability to swap providers without touching the controller. Environment promotion from dev to production is unsafe as-is.
- Severity: High
- Recommendation: Move all credentials and endpoint URLs to `.env` and bind via `config/services.php`. Wrap the provider call behind a `PaymentGatewayInterface` to decouple the controller from the specific provider.
- Expected benefit: Safe secret management, clean environment separation, and provider portability.

### B-5. Student authentication is only an IC-number lookup
- Major category: Implementation/Backend
- Secondary lens: Contract/Precondition; Defensive Programming
- Source: Codex (confirmed by cross-check)
- Location: `TVPSS-MAIN/app/Http/Controllers/StudentController.php:19-31`; `TVPSS-MAIN/routes/studentRoutes.php:9-13`; `TVPSS-MAIN/app/Http/Middleware/StudentSessionCheck.php:13-20`
- Problem: Student login validates only `ic_num`, retrieves the first matching student, and stores the IC number in session. `StudentSessionCheck` only checks whether that session key is present. There is no password, token, OTP, throttling, or second factor in the student authentication path.
- Evidence:
  - `StudentController::login()` validates `ic_num` only, calls `Student::where('ic_num', ...)->first()`, then `session(['ic_num' => $student->ic_num])`.
  - `StudentSessionCheck` checks only `session()->has('ic_num')`.
- Why it matters: Any user who knows or guesses a valid IC number has full access to that student's crew-application data. This is an identity contract failure on the system's only student-facing authentication boundary.
- Severity: High
- Recommendation: Replace IC-only session with real authentication (password, one-time verified link, or OTP flow) plus rate throttling and session-bound identity checks.
- Expected benefit: Protects student identity and makes the student subsystem's trust assumptions defensible.

### B-6. Duplicate follow-up workflow logic across controller roles
- Major category: Implementation/Backend
- Secondary lens: Function Reuse; Maintainability/Evolvability
- Source: Copilot (missed by Codex)
- Location: `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php::saveFollowUp()`; `TVPSS-MAIN/app/Http/Controllers/PPDAdminController.php::saveFollowUp()`
- Problem: Near-identical validation, status guard, file storage, and `EqFollowUp::create` logic appears in both controllers. Any bug fix or requirement change must be applied to two separate implementations.
- Evidence:
  - Same validation shape, same status guard condition, same `Storage::putFileAs()` pattern, same `EqFollowUp::create` call in both controllers.
- Why it matters: Duplication creates a maintenance trap. Bug fixes applied to one copy are likely to be missed in the other. This is the most visible instance of a broader pattern of scattered, duplicated workflow logic.
- Severity: Medium
- Recommendation: Extract a shared `CreateEquipmentFollowUpAction` service class with role-specific authorization injected via policies. Both controllers invoke the shared action.
- Expected benefit: Single source of truth for follow-up creation, cleaner authorization model, and easier maintenance.

### B-7. Route contracts are inconsistent across binding style, parameter naming, and route naming
- Major category: Implementation/Backend
- Secondary lens: Contract/Precondition; Maintainability/Evolvability
- Source: Both (different aspects); cross-check confirmed
- Location: `TVPSS-MAIN/routes/schoolAdminRoutes.php`; `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php` (equipment methods); `TVPSS-MAIN/routes/ppdAdminRoutes.php`; `TVPSS-MAIN/routes/stateAdminRoutes.php`
- Problem: Three distinct contract failures at the routing layer:
  (a) Equipment show route uses `{id}` but controller signature uses typed `Equipment $equipment` binding — auto-resolution fails silently.
  (b) `equipmentUpdate()` redirects to `route('equipment.edit')` without the required `{equipment}` parameter — a nominally successful update ends in a routing exception.
  (c) `ppdAdminRoutes.php` and `stateAdminRoutes.php` both define `schoolInfo.approveTVPSS` and `schoolInfo.rejectTVPSS` — last-registered wins, silently breaking the loser's URL generation.
- Evidence:
  - Route: `equipment/{id}` → Controller: `equipmentShow(Equipment $equipment)` (typed binding with mismatched parameter name).
  - `equipmentUpdate()` returns `redirect()->route('equipment.edit')` with no parameter; route requires `{equipment}`.
  - Both PPD and State route files define the same named routes without subsystem namespacing.
- Why it matters: Route contracts are the interface between HTTP and application logic. These three failures produce 404/500 errors on specific code paths and ambiguous URL generation as the system evolves.
- Severity: Medium
- Recommendation: Standardize on typed route-model binding with consistent parameter names. Add the `$equipment->id` parameter to the `equipmentUpdate()` redirect. Namespace route names per subsystem (`ppd.schoolInfo.*`, `state.schoolInfo.*`).
- Expected benefit: Predictable endpoint contracts, fewer production-time routing defects, and stable URL generation across modules.

### B-8. FormRequest validation is duplicated inside controllers
- Major category: Implementation/Backend
- Secondary lens: Contract/Precondition; Function Reuse
- Source: Copilot (confirmed by cross-check)
- Location: `TVPSS-MAIN/app/Http/Controllers/UserController.php`; `TVPSS-MAIN/app/Http/Requests/User/StoreUserRequest.php`; `TVPSS-MAIN/app/Http/Requests/User/UpdateUserRequest.php`
- Problem: Controller methods type-hinted with dedicated FormRequest classes still call `$request->validate(...)` inline, duplicating the validation definitions.
- Evidence:
  - `UserController::store()` receives `StoreUserRequest` but also calls `$request->validate(...)`.
  - `UserController::update()` receives `UpdateUserRequest` but also calls `$request->validate(...)`.
- Why it matters: Two validation definitions for the same input can diverge over time. The contract that the FormRequest represents becomes unreliable.
- Severity: Medium
- Recommendation: Remove inline `validate()` calls from controllers that already use dedicated FormRequest classes. Keep all validation in the FormRequest and ensure `authorize()` is implemented.
- Expected benefit: Single validation contract per input, clearer caller/callee responsibilities.

### B-9. Student session middleware redirects to a POST route
- Major category: Implementation/Backend
- Secondary lens: Exception Contract; Defensive Programming
- Source: Copilot (confirmed by cross-check)
- Location: `TVPSS-MAIN/app/Http/Middleware/StudentSessionCheck.php`; `TVPSS-MAIN/routes/studentRoutes.php`
- Problem: `StudentSessionCheck` redirects unauthenticated students to `student.login`, which maps to the POST endpoint. The GET login page is at `student.showLogin`. Browsers following the redirect will GET the POST route, producing a 405 Method Not Allowed or similar failure.
- Evidence:
  - `StudentSessionCheck.php` calls `redirect(route('student.login'))`.
  - Student route file defines `student.login` as a POST route; the login page is a separate GET route (`student.showLogin`).
- Why it matters: The error path for any protected student route is broken. A student who loses their session or navigates directly to a protected URL cannot recover gracefully.
- Severity: Medium
- Recommendation: Change the redirect target in `StudentSessionCheck` to `student.showLogin`. Codify expected route-method contracts in feature tests.
- Expected benefit: Robust session-expiry handling and correct error-path navigation.
