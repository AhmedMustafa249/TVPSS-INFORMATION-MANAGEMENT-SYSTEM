# TVPSS-MAIN Documentation Issues

## Working Notes
- Findings will be added here during SRS/SDD vs code comparison.

## Early Documentation Observations
- `TVPSS-MAIN/README.md` is still the stock Laravel README rather than project documentation.
- `Software Documents/SDD.md` claims additional modules not clearly covered in the SRS scope sections.

## Findings

### 1. Crew application use cases are richer than the implemented workflow
- Major category: Documentation/Use Case Mismatch
- Secondary lens: Contract/Postcondition; Maintainability/Evolvability
- Location: `Software Documents/SRS.md`, `TVPSS-MAIN/app/Http/Controllers/StudentController.php`, `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php`, `TVPSS-MAIN/resources/js/Pages/5-Students/ApplyCrew.jsx`, `TVPSS-MAIN/resources/js/Pages/5-Students/ResultApply.jsx`, `TVPSS-MAIN/resources/js/Pages/4-SchoolAdmin/StudentManagement/approveStudCrew.jsx`
- Problem: The SRS documents a richer contract for UC009/UC011/UC012 than the code implements.
- Evidence:
  - SRS states duplicate applications must be blocked, open positions should be shown with descriptions, rejection requires a reason, students receive notifications, tests/interviews are scheduled, and result pages include feedback/acceptance details.
  - `ApplyCrew.jsx` exposes only a static position dropdown.
  - `StudentController::applyCrewSubmit()` inserts a record immediately and has no duplicate check, eligibility check, scheduling, or notification step.
  - `approveStudCrew.jsx` only exposes approve/reject buttons; `SchoolAdminController::rejectStudcrew()` stores no rejection reason and triggers no student notification.
  - `ResultApply.jsx` shows only basic fields and does not surface evaluator feedback, interview details, or acceptance letters.
- Severity: High
- Recommendation: Either implement the documented alternate/exception flows and postconditions, or reduce the SRS to match the delivered system.
- Expected benefit: Restores traceability between requirements, UI, and backend behavior.

### 2. The documented module set is internally inconsistent and drifts from the repo
- Major category: Documentation/Architecture Issue
- Secondary lens: Subsystem Reuse; Architecture/Boundary
- Location: `Software Documents/SRS.md`, `Software Documents/SDD.md`, `TVPSS-MAIN/routes/donationRoutes.php`, `TVPSS-MAIN/routes/ppdAdminRoutes.php`
- Problem: The SRS scope describes four main modules, while the SDD says there are "four main modules" and then lists six, adding donation management and equipment report management. The codebase does include donation and PPD equipment features, but the requirements scope is not stable across documents.
- Evidence:
  - `SRS.md` scope lists four modules: dashboard/administration, school information management, school version management, and student achievement management.
  - `SDD.md` scope says "There are four main modules" and then lists six including donation and equipment report management.
  - The code contains `routes/donationRoutes.php` and PPD equipment management routes in `routes/ppdAdminRoutes.php`.
- Severity: Medium
- Recommendation: Normalize the official subsystem list across SRS, SDD, README, and route/module naming.
- Expected benefit: Clearer architectural boundaries and more reliable future maintenance.

### 3. PWA and sequence-diagram claims are not backed by repository artifacts
- Major category: Documentation/Diagram Discrepancy
- Secondary lens: Application System Reuse; Maintainability/Evolvability
- Location: `Software Documents/SRS.md`, `Software Documents/SDD.md`, `TVPSS-MAIN/resources/views/app.blade.php`, repo-wide search results
- Problem: The documents describe the system as a PWA and claim detailed sequence-diagram coverage, but the repository does not contain PWA assets or usable sequence-diagram artifacts.
- Evidence:
  - `SRS.md` and `SDD.md` both say the system will be designed as a PWA.
  - Repo search found no service worker, web manifest, or PWA bootstrap code, and `resources/views/app.blade.php` contains no manifest link.
  - `SDD.md` sequence-diagram section is mostly repeated figure labels like `Figure 4.4`, with no actual sequence content preserved in Markdown, and there are no corresponding diagram image assets under `Software Documents`.
- Severity: Medium
- Recommendation: Either add the missing PWA/diagram artifacts to the repo or revise the documents to describe the delivered browser application honestly.
- Expected benefit: Accurate platform claims and reviewable design documentation.

### 4. Architecture documentation claims strong role-based access control that the code does not enforce
- Major category: Documentation/Architecture Issue
- Secondary lens: Architecture/Boundary; Defensive Programming
- Location: `Software Documents/SDD.md`, `TVPSS-MAIN/routes/web.php`, `TVPSS-MAIN/bootstrap/app.php`
- Problem: The SDD states that role-based access control ensures users only access permitted areas, but the route configuration does not actually apply role middleware.
- Evidence:
  - `SDD.md` states the logical and algorithm viewpoints enforce role-based permissions and proper access control.
  - `routes/web.php` groups all admin route files under shared `auth`/`verified` middleware.
  - `bootstrap/app.php` has the role middleware commented out.
- Severity: High
- Recommendation: Bring the implementation up to the documented architecture or revise the architecture section to reflect current limitations.
- Expected benefit: Better trust in the documentation and fewer false assumptions by maintainers.
