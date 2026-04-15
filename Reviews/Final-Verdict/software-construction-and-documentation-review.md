# TVPSS-MAIN Final Software Construction and Documentation Review

Final adjudication across Codex findings, Copilot findings, and Copilot cross-check of Codex. Static review only — `vendor/` and `node_modules/` are absent from the workspace snapshot.

---

## 1. Top 5 Most Important Problems

1. Authorization is structurally absent — role middleware is disabled, all admin routes are accessible to any authenticated user, and the mechanism to fix this has broken redirect targets that would cause immediate failures if re-enabled.
2. The persistence layer has silent invariant failures — the achievement schema migration is broken at definition level, and the MongoDB-default plus SQL-style migration strategy means no foreign key constraint is ever enforced by the database.
3. Payment integration has plaintext credentials and a dev-environment URL hard-coded in a controller with no environment separation and no adapter interface.
4. `SchoolAdminController` has collapsed eight to ten subsystems into 1,174 lines — this is the structural bottleneck for every high-priority fix in the school-admin domain.
5. The crew application workflow (the system's central student-facing feature) does not implement its documented use case contract — no duplicate check, no rejection reason, no notifications, no scheduling, no acceptance artifacts.

---

## 2. Implementation Issues

### Frontend Issues

- Title: Status vocabulary mismatch in crew application result UI
- Major Category: Implementation/Frontend
- Secondary Lens: Contract/Postcondition
- Location: `resources/js/Pages/5-Students/ResultApply.jsx:123-129,236-270`; `app/Http/Controllers/StudentController.php:76-80`; `app/Http/Controllers/SchoolAdminController.php:924-939`
- Problem: Backend writes `Permohonan Belum Diproses`, `Approved`, `Rejected`. Modal logic in `ResultApply.jsx` checks `Diluluskan` and `Dalam Proses`. Badge and modal operate on different vocabularies; the same record can render a correct badge with an incorrect modal title and wrong CTA.
- Why it matters: Student-facing behavior is wrong on the happy path. The postcondition of the approval flow is not correctly observable to the student.
- Evidence: Confirmed by both reviewers and the cross-check. String mismatch is verifiable directly in source.
- Severity: Medium
- Recommendation: Define one canonical crew-application status enum/constants and consume it in both PHP controllers and `ResultApply.jsx`.

### Backend Issues

- Title: Authorization absent as a structural boundary — and the remediation path is blocked
- Major Category: Implementation/Backend
- Secondary Lens: Architecture/Boundary; Defensive Programming
- Location: `bootstrap/app.php:14-18`; `routes/web.php:31-46`; `SchoolAdminController.php:244-313,918-952`; `PPDAdminController.php:162-205,278-282`
- Problem: `CheckRole` is commented out. All role-specific route files load under a single auth group. Controller methods use global `findOrFail()` without tenant scoping. Additionally, `CheckRole` redirects to undefined route names — re-enabling it without fixing those targets causes immediate runtime failures.
- Why it matters: Every admin endpoint is accessible to any authenticated user. The role-based access model is aspirational, not implemented. The natural first fix is itself broken.
- Evidence: Confirmed by both reviewers and the cross-check at high confidence.
- Severity: High

- Title: Achievement persistence invariant is broken at the migration level
- Major Category: Implementation/Backend
- Secondary Lens: Contract/Invariant; Defensive Programming
- Location: `database/migrations/2024_12_27_193450_create_student_achievements_table.php`; `SchoolAdminController.php` (achievement creation); `app/Models/StudentAchievement.php`
- Problem: Migration defines `$table->id()` (bigint) but controller writes string IDs (`PS0001`). Migration declares a foreign key on `student_id` without defining that column. Because the database is MongoDB, the migration "succeeds" but the constraint is never enforced, making the broken schema invisible.
- Why it matters: Data integrity failures accumulate silently. The persistence contract for this module was never valid.
- Evidence: Confirmed by Copilot and cross-check. Missed by Codex.
- Severity: High

- Title: MongoDB default with SQL-style migrations creates a silent correctness gap
- Major Category: Implementation/Backend
- Secondary Lens: Architecture/Boundary; Application System Reuse
- Location: `config/database.php`; all migration files; all models
- Problem: `config/database.php` defaults to MongoDB. Models extend `MongoDB\Laravel\Eloquent\Model`. Migrations use SQL-style FK declarations that MongoDB never processes. Every relational constraint in every migration is silently ignored at runtime.
- Why it matters: Developers cannot trust that any FK constraint in a migration file is actually enforced. This undermines correctness analysis of the entire data layer.
- Evidence: Confirmed by Copilot and cross-check. Missed by Codex.
- Severity: High

- Title: Payment integration has hard-coded secrets and a dev-environment URL
- Major Category: Implementation/Backend
- Secondary Lens: Application System Reuse; Defensive Programming
- Location: `app/Http/Controllers/paymentController.php`
- Problem: `userSecretKey`, `categoryCode`, and `https://dev.toyyibpay.com` are literal constants in the controller. No adapter interface. Dev endpoint in production-path code.
- Why it matters: Active security risk, portability failure, and unsafe environment promotion path.
- Evidence: Confirmed by Copilot and cross-check. Missed by Codex.
- Severity: High

- Title: Student authentication is only an IC-number lookup
- Major Category: Implementation/Backend
- Secondary Lens: Contract/Precondition; Defensive Programming
- Location: `app/Http/Controllers/StudentController.php:19-31`; `app/Http/Middleware/StudentSessionCheck.php:13-20`
- Problem: Login validates only `ic_num`, loads first match, writes to session. Session check only confirms the key exists. No password, token, throttling, or second factor.
- Why it matters: Any user who knows a valid IC number has full access to that student's data. Identity contract failure on the student authentication boundary.
- Evidence: Confirmed by both reviewers at high confidence.
- Severity: High

- Title: `SchoolAdminController` is a god controller
- Major Category: Implementation/Backend
- Secondary Lens: Architecture/Boundary; Maintainability/Evolvability
- Location: `app/Http/Controllers/SchoolAdminController.php:27-1143`; `routes/schoolAdminRoutes.php:7-79`
- Problem: One 1,174-line controller owns equipment, follow-ups, locations, school profile, TVPSS versioning, student management, crew approval, achievements, donations, and dashboard statistics. Contains inline domain rules (`checkTVPSSVersion()`).
- Why it matters: Every high-priority fix in the school-admin domain touches this file. Change amplification is unavoidable until the controller is split.
- Evidence: Confirmed by both reviewers at high confidence.
- Severity: High

- Title: Route contracts are inconsistent across binding style, parameter naming, and route naming
- Major Category: Implementation/Backend
- Secondary Lens: Contract/Precondition; Maintainability/Evolvability
- Location: `routes/schoolAdminRoutes.php`; `SchoolAdminController.php` (equipment methods); `routes/ppdAdminRoutes.php`; `routes/stateAdminRoutes.php`
- Problem: (a) Equipment show route uses `{id}` but controller uses typed `Equipment $equipment` binding. (b) `equipmentUpdate()` redirects to a named route without the required parameter. (c) PPD and State route files both define `schoolInfo.approveTVPSS` and `schoolInfo.rejectTVPSS` without namespace separation.
- Why it matters: Routing exceptions on success paths and ambiguous URL generation as the system evolves.
- Evidence: Both reviewers confirmed different aspects; cross-check confirmed route name collision.
- Severity: Medium

- Title: Duplicate follow-up workflow logic across controller roles
- Major Category: Implementation/Backend
- Secondary Lens: Function Reuse; Maintainability/Evolvability
- Location: `SchoolAdminController::saveFollowUp()`; `PPDAdminController::saveFollowUp()`
- Problem: Near-identical validation, status guard, file storage, and `EqFollowUp::create` logic in two controllers.
- Why it matters: Bug fixes applied to one copy are likely to be missed in the other.
- Evidence: Confirmed by Copilot. Missed by Codex.
- Severity: Medium

- Title: FormRequest validation is duplicated inside controllers
- Major Category: Implementation/Backend
- Secondary Lens: Contract/Precondition; Function Reuse
- Location: `UserController.php`; `StoreUserRequest.php`; `UpdateUserRequest.php`
- Problem: Controllers type-hinted with FormRequest classes still call `$request->validate(...)` inline, duplicating the validation definitions.
- Evidence: Confirmed by Copilot and cross-check.
- Severity: Medium

- Title: Student session middleware redirects to a POST route
- Major Category: Implementation/Backend
- Secondary Lens: Exception Contract; Defensive Programming
- Location: `app/Http/Middleware/StudentSessionCheck.php`; student route file
- Problem: `StudentSessionCheck` redirects to `student.login` (POST). The GET login page is `student.showLogin`. Browsers following the redirect receive a method mismatch failure.
- Evidence: Confirmed by Copilot and cross-check.
- Severity: Medium

---

## 3. Documentation Issues

### Missing Use Cases
- Title: Donation and equipment-report modules have no SRS use cases
- Location: `SRS.md:170-178`; `routes/donationRoutes.php`; `routes/ppdAdminRoutes.php`
- Problem: Two implemented modules have no requirements traceability in the SRS.
- Severity: Medium

- Title: PWA capability is documented but has no implementation artifacts
- Location: `SRS.md`; `SDD.md`; `resources/views/app.blade.php`
- Problem: No service worker, manifest, or PWA bootstrap exists in the repository.
- Severity: Medium

### Use Case Mismatches
- Title: Crew application workflow does not implement the documented use case contract
- Location: `SRS.md:1386-1473,1585-1747` (UC009/UC011/UC012); `StudentController.php:61-118`; `SchoolAdminController.php:924-939`
- Problem: Duplicate prevention, rejection reasons, notifications, scheduling, and acceptance artifacts are documented but absent from the implementation.
- Severity: High

### Architecture Documentation Issues
- Title: SDD describes role enforcement and modular structure that do not exist in the code
- Location: `SDD.md:1415-1433,1818-1847,2055-2069`; `routes/web.php:31-46`; `SchoolAdminController.php:27-1143`
- Problem: SDD presents a role-enforced, modular architecture. The code has disabled role enforcement and a god controller absorbing most school-admin behavior.
- Severity: High

- Title: SRS and SDD disagree on the official module inventory
- Location: `SRS.md:170-178`; `SDD.md:181-190`
- Problem: SRS names four modules; SDD claims four but lists six. Code implements six. No single document is authoritative.
- Severity: Medium

---

## 4. Reuse Review
- Application System Reuse: Low — payment integration is hard-coded to one provider and one environment. No adapter interface. PWA claimed but absent.
- Subsystem Reuse: Low — role subsystems are not cleanly bounded. All admin functionality is reachable through the same auth group. Extraction of any subsystem requires first establishing the boundaries that do not currently exist.
- Module/Object Reuse: Low to Moderate — Eloquent models and PHP enums are somewhat reusable. Controller logic is highly role- and route-specific with no service layer to mediate reuse.
- Function Reuse: Low — follow-up creation, school lookup, and status-handling logic are duplicated across controllers rather than centralized.

---

## 5. Contract and Defensive Programming Review
- Preconditions are weak at identity and role boundaries — student access is IC-only, admin role checks are not enforced at route boundaries, and ownership scoping is inconsistent across mutation endpoints.
- Postconditions are violated in several flows — equipment update can redirect to an invalid route, and the documented crew-application postconditions are not met.
- Invariants are not enforced — one-pending-application-per-student, canonical status vocabulary, tenant ownership, and achievement ID strategy are all unprotected.
- Exception behavior is inconsistent — the codebase mixes `abort(403)`, flash redirects, JSON errors, and broken redirect targets such as `some.error.page` in `StateAdminController`.
- Schema-level invariants are not enforced — the MongoDB default means no FK constraint from any migration is processed at the database layer.
- Assertions and regression protection are minimal — the test suite is mostly framework scaffold tests with no coverage of the domain flows reviewed here.

---

## 6. Architecture and Modular Design Smells
- Layer leakage: controllers combine orchestration, validation, domain decisions, file storage, notification logic (absent but needed), and response composition.
- Tight coupling: domain workflows are directly coupled to framework request/session/filesystem APIs with no service layer to mediate.
- Duplicated responsibilities: follow-up creation, school lookup, and status semantics are redefined across multiple controllers.
- God module: `SchoolAdminController` is the dominant design smell.
- Unstable interfaces: duplicate named routes across subsystems and inconsistent route parameter conventions.
- Documentation/code drift: SRS, SDD, and implementation do not describe the same module set, access model, or workflow behavior.
- Persistence strategy ambiguity: MongoDB runtime + SQL migration semantics with no explicit commitment to either.

---

## 7. Long-Term Improvements
- Fix `CheckRole` redirect targets, then reinstate and enforce role middleware per route group with full ownership scoping.
- Commit to one persistence strategy (MongoDB document model or relational SQL) and remove all artifacts from the other.
- Decompose `SchoolAdminController` into bounded-context controllers with domain rules extracted into services.
- Make crew application a proper bounded workflow with canonical statuses, rejection reasons, notifications, and result artifacts.
- Reconcile SRS and SDD into one stable module inventory and restore usable sequence diagrams in the repository.
- Add feature tests for role access boundaries, crew workflow postconditions, and TVPSS version approval.

---

## 8. Strengths Found
- Enum-backed state modeling exists in `TVPSSVersion` — a sound foundation for stricter status contracts that can be extended to other domain states.
- FormRequest classes are already in place and can become the contract backbone with limited refactoring effort.
- Role-specific route files reflect the correct architectural intent — the separation at the file level is right; the failure is at the enforcement level.
- Inertia.js separation between server-rendered props and React pages is consistently applied — this is a clean boundary that limits UI/API surface area.
- Transactions are used in multiple write-heavy flows, providing some protection against partial-write failures.

---

## 9. Final Verdict

- Software construction maturity: Low
- Documentation alignment maturity: Low
- Reuse maturity: Low
- Most reusable part of the project: enum-backed domain model pieces and existing FormRequest scaffolding
- Least reusable part of the project: the school-admin controller/route/page cluster and the payment controller
- Biggest blocker to maintainability: `SchoolAdminController` concentrating eight to ten subsystems in one file
- Biggest blocker to reuse: authorization and ownership logic scattered across controller methods with no centralized policy or service layer
- Biggest blocker to architectural clarity: SDD presents a modular, role-enforced architecture that does not exist in the code — future design decisions are anchored to a false baseline
- Biggest construction risk: authorization is structurally absent and the natural remediation path (re-enable `CheckRole`) has a hidden dependency that must be resolved first
- Biggest documentation risk: UC009/UC011/UC012 describe a crew workflow that is not implemented — the most documented feature has the largest gap between specification and delivery
