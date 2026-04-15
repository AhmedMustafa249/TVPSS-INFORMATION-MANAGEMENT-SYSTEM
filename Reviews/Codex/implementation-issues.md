# TVPSS-MAIN Implementation Issues

## Working Notes
- Findings will be added here during frontend and backend review.

## Findings

### 1. Server-side authorization is incomplete and inconsistent
- Major category: Implementation/Backend
- Secondary lens: Architecture/Boundary; Defensive Programming
- Location: `TVPSS-MAIN/routes/web.php`, `TVPSS-MAIN/bootstrap/app.php`, `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php`, `TVPSS-MAIN/app/Http/Controllers/PPDAdminController.php`
- Problem: All admin route files are loaded under `auth` and `verified`, but no active role middleware is applied. Controller methods then mix scoped and unscoped record access, so authorization depends on ad hoc query choices rather than a stable contract.
- Evidence:
  - `routes/web.php` includes `schoolAdminRoutes.php`, `ppdAdminRoutes.php`, `stateAdminRoutes.php`, and `superAdminRoutes.php` inside a shared `Route::middleware(['auth', 'verified'])` group.
  - `bootstrap/app.php` has `CheckRole` commented out.
  - `SchoolAdminController::saveFollowUp()` loads equipment with `Equipment::findOrFail($equipmentId)` and `getFollowUps()` returns follow-ups by equipment id without school scoping.
  - `SchoolAdminController::editStudcrew()`, `approveStudcrew()`, `rejectStudcrew()`, and `destroy()` all operate on global `StudCrew::findOrFail($id)`.
  - `PPDAdminController::editEquipment()`, `updateEquipment()`, `saveFollowUp()`, and `deleteEquipment()` load equipment by id without district scoping.
- Severity: High
- Recommendation: Enforce role middleware or policies at route/controller boundaries and require all record fetches to be tenant-scoped (school, district, state) before mutation.
- Expected benefit: Restores access-control contracts, reduces cross-role/cross-school data exposure, and simplifies reasoning about permissions.

### 2. Student authentication is only an IC-number lookup
- Major category: Implementation/Backend
- Secondary lens: Contract/Precondition; Defensive Programming
- Location: `TVPSS-MAIN/app/Http/Controllers/StudentController.php`
- Problem: Student login validates only `ic_num`, loads the first matching student, and writes that value directly into the session. There is no password, token, rate limiting, or secondary proof of identity.
- Evidence:
  - `StudentController::login()` only validates `ic_num`, performs `Student::where('ic_num', ...)->first()`, then calls `session(['ic_num' => $student->ic_num])`.
  - The protected student area in `routes/studentRoutes.php` relies on `StudentSessionCheck`, which only checks whether the session contains `ic_num`.
- Severity: High
- Recommendation: Replace the IC-only session with a real student authentication flow or a one-time verified access mechanism, and add throttling plus session-bound identity checks.
- Expected benefit: Prevents trivial impersonation of students and makes the student-facing workflow trustworthy.

### 3. SchoolAdminController has become a god controller
- Major category: Implementation/Backend
- Secondary lens: Architecture/Boundary; Maintainability/Evolvability
- Location: `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php`, `TVPSS-MAIN/routes/schoolAdminRoutes.php`
- Problem: One 1174-line controller owns equipment, equipment follow-ups, locations, school information, TVPSS version logic, student CRUD, student crew approval, achievements, donations, and dashboard statistics. This collapses multiple subsystem boundaries into one change surface.
- Evidence:
  - `routes/schoolAdminRoutes.php` maps most school-admin features to a single controller.
  - `SchoolAdminController` contains methods from `equipmentIndex()` through `countStudCrewJawatan()` spanning distinct domains, including an inline `checkTVPSSVersion()` rules engine.
- Severity: High
- Recommendation: Split the controller by module or bounded context and move version-calculation plus approval rules into dedicated services.
- Expected benefit: Smaller change sets, clearer ownership, easier testing, and less architecture erosion.

### 4. Application result UI uses inconsistent status vocabularies
- Major category: Implementation/Frontend
- Secondary lens: Contract/Postcondition; Maintainability/Evolvability
- Location: `TVPSS-MAIN/app/Http/Controllers/StudentController.php`, `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php`, `TVPSS-MAIN/resources/js/Pages/5-Students/ResultApply.jsx`
- Problem: Backend code stores statuses as `Permohonan Belum Diproses`, `Approved`, and `Rejected`, but the modal logic in `ResultApply.jsx` checks `Diluluskan` and `Dalam Proses`. The same record can therefore receive a correct badge but an incorrect modal outcome.
- Evidence:
  - `StudentController::applyCrewSubmit()` sets `Permohonan Belum Diproses`.
  - `SchoolAdminController::approveStudcrew()` and `rejectStudcrew()` set `Approved` and `Rejected`.
  - `ResultApply.jsx` badge colors handle `Approved` and `Permohonan Belum Diproses`, while modal title and print action check `Diluluskan` and `Dalam Proses`.
- Severity: Medium
- Recommendation: Centralize crew-application status values and consume the same canonical enum/constants in both backend and frontend.
- Expected benefit: Correct student-facing behavior and less fragile UI branching.

### 5. Equipment update success path can fail on redirect
- Major category: Implementation/Backend
- Secondary lens: Exception Contract
- Location: `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php`
- Problem: `equipmentUpdate()` redirects to `route('equipment.edit')` without the required route parameter.
- Evidence:
  - Route definition expects `/equipment/{equipment}/edit`.
  - `equipmentUpdate()` returns `redirect()->route('equipment.edit')->with('success', ...)`.
- Severity: Medium
- Recommendation: Redirect with the current equipment id, or redirect to the list page.
- Expected benefit: Preserves the success postcondition after updating equipment instead of risking a routing exception.
