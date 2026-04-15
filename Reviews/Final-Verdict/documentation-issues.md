# TVPSS-MAIN Final Verdict — Documentation Issues

## Missing Use Cases

### D-2. Donation and equipment-report modules have no use cases in the SRS
- Major category: Documentation/Missing Use Case
- Secondary lens: Subsystem Reuse; Architecture/Boundary
- Source: Codex (confirmed by cross-check)
- Location: `Software Documents/SRS.md:170-178`; `Software Documents/SDD.md:181-190`; `TVPSS-MAIN/routes/donationRoutes.php`; `TVPSS-MAIN/routes/ppdAdminRoutes.php`
- Problem: The SRS scope defines four modules. The SDD claims "four main modules" but then lists six, adding donation management and equipment report management. The codebase contains route files and controller logic for both additional modules. Neither module has any corresponding use case, alternate flow, or requirement in the SRS.
- Evidence:
  - `SRS.md` scope section names: dashboard/administration, school information management, school version management, student achievement management.
  - `SDD.md` scope section names: the above four plus donation management and equipment report management.
  - `routes/donationRoutes.php` exists with donation-related routes.
  - `routes/ppdAdminRoutes.php` contains PPD equipment-management routes.
- Why it matters: Two modules are implemented without any requirements traceability. Future changes to donation or equipment-report behavior have no documented contract to reference or validate against.
- Severity: Medium
- Recommendation: Either add SRS use cases for donation management and equipment reporting (with alternate and exception flows), or formally declare them out of scope in the SRS and remove the associated SDD claims.
- Expected benefit: A stable, trustworthy module inventory across SRS, SDD, and code.

### D-3. PWA capability is documented but has no implementation artifacts in the repository
- Major category: Documentation/Missing Use Case (platform claim)
- Secondary lens: Application System Reuse; Maintainability/Evolvability
- Source: Codex (confirmed by cross-check)
- Location: `Software Documents/SRS.md`; `Software Documents/SDD.md`; `TVPSS-MAIN/resources/views/app.blade.php`
- Problem: Both the SRS and SDD describe the system as a Progressive Web App (PWA). No service worker, web app manifest, or PWA bootstrap configuration exists in the repository. `app.blade.php` contains no manifest link or PWA registration.
- Evidence:
  - SRS and SDD both reference PWA as a system characteristic.
  - No `manifest.json`, `service-worker.js`, or equivalent asset found in the repository.
  - `resources/views/app.blade.php` has no `<link rel="manifest">` or service worker registration.
- Why it matters: Presenting the system as a PWA in documentation is a false platform claim. Reviewers and stakeholders evaluating offline capability, installability, or mobile app behavior will be misled.
- Severity: Medium
- Recommendation: Either implement the minimum PWA requirements (manifest, service worker, HTTPS meta, installability) or remove the PWA claim from both SRS and SDD.
- Expected benefit: Accurate platform description and honest stakeholder expectations.

---

## Use Case Mismatches

### D-4. Crew application workflow does not implement the documented use case contract
- Major category: Documentation/Use Case Mismatch
- Secondary lens: Contract/Postcondition; Maintainability/Evolvability
- Source: Codex (confirmed by both Copilot cross-check and independent Copilot review)
- Location: `Software Documents/SRS.md:1386-1473,1585-1747` (UC009, UC011, UC012); `TVPSS-MAIN/app/Http/Controllers/StudentController.php:61-118`; `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php:924-939`; `TVPSS-MAIN/resources/js/Pages/5-Students/ApplyCrew.jsx`; `TVPSS-MAIN/resources/js/Pages/5-Students/ResultApply.jsx`; `TVPSS-MAIN/resources/js/Pages/4-SchoolAdmin/StudentManagement/approveStudCrew.jsx`
- Problem: UC009/UC011/UC012 in the SRS specify the following behaviors that are absent from the implementation:
  - Duplicate application prevention (a student cannot apply twice for the same position)
  - Rejection reason capture (admin must provide a reason when rejecting)
  - Student notification on approval or rejection
  - Interview/scheduling logic
  - Structured acceptance artifacts shown to the student on the result page
  - Evaluator feedback surfaced in the result view
  The implementation stores a status string and renders basic views. None of the documented alternate or exception flows exist in code.
- Evidence:
  - `StudentController::applyCrewSubmit()` inserts a record with no duplicate check or eligibility guard.
  - `SchoolAdminController::rejectStudcrew()` updates status to `Rejected` with no rejection-reason field or notification trigger.
  - `ApplyCrew.jsx` exposes only a static position dropdown.
  - `ResultApply.jsx` shows only basic status fields — no evaluator feedback, interview details, or acceptance document.
- Why it matters: This is the system's primary student-facing workflow and the most heavily documented use case cluster. The gap between the SRS contract and the implementation is large enough that the use cases cannot function as implementation guidance or acceptance criteria.
- Severity: High
- Recommendation: Either implement the documented alternate and exception flows (duplicate check, rejection reason, notification, result artifacts) or formally reduce the SRS use cases to reflect delivered behavior. Do not leave a wide unacknowledged gap between the two.
- Expected benefit: Restores requirements traceability for the system's core workflow and gives maintainers a reliable contract to work from.

---

## Architecture Issues

### D-5. SDD describes role enforcement and modular subsystem structure that does not exist in the code
- Major category: Documentation/Architecture Issue
- Secondary lens: Architecture/Boundary; Defensive Programming
- Source: Codex (confirmed by both Copilot cross-check and independent Copilot review)
- Location: `Software Documents/SDD.md:1415-1433,1818-1847,2055-2069`; `TVPSS-MAIN/routes/web.php:31-46`; `TVPSS-MAIN/bootstrap/app.php:14-18`; `TVPSS-MAIN/app/Http/Controllers/SchoolAdminController.php:27-1143`
- Problem: The SDD presents: (a) role-based access control ensuring users only access permitted areas; (b) a modular controller structure with clear subsystem-to-controller mapping; (c) a logical architecture where each role has bounded responsibilities. The code has: (a) role middleware disabled; (b) one 1,174-line controller absorbing eight to ten school-admin subsystems; (c) all admin routes accessible to any authenticated user.
- Evidence:
  - SDD logical viewpoint and class diagram describe modular controllers and role-enforced boundaries.
  - `bootstrap/app.php` has `CheckRole` commented out.
  - `SchoolAdminController.php` spans lines 27–1143 and owns equipment, follow-ups, locations, school profile, TVPSS versioning, students, crew approval, achievements, donations, and dashboard statistics.
  - `routes/web.php` groups all role-specific route files under a single auth group with no per-role enforcement.
- Why it matters: The SDD functions as the authoritative architectural description for this project. Any future developer, reviewer, or stakeholder reading it will form false assumptions about what the system enforces. Design decisions and refactoring work will be anchored to an inaccurate baseline.
- Severity: High
- Recommendation: After any refactoring, update the SDD to reflect actual code structure. If refactoring is not imminent, annotate the affected SDD sections explicitly: mark what is intended design versus current implementation state.
- Expected benefit: Eliminates misleading architectural claims and gives future maintainers an honest design baseline.

### D-6. SRS and SDD disagree on the official module inventory
- Major category: Documentation/Architecture Issue
- Secondary lens: Subsystem Reuse; Architecture/Boundary
- Source: Codex (confirmed by cross-check)
- Location: `Software Documents/SRS.md:170-178`; `Software Documents/SDD.md:181-190`
- Problem: The SRS and SDD were written by different teams and were never reconciled. The SRS defines four modules. The SDD claims four but lists six. The code contains routes and controllers for six. There is no single document that correctly describes the full module set.
- Evidence:
  - SRS: four modules (dashboard/administration, school information, school version, student achievement).
  - SDD: claims four, lists six (adding donation management, equipment report management).
  - Codebase: routes and controllers for all six.
- Why it matters: Subsystem boundaries are not stable across artifacts. There is no single trustworthy requirements baseline for understanding what the system is supposed to do and which modules are in or out of scope.
- Severity: Medium
- Recommendation: Produce a single reconciled module inventory — six modules if the implementation is authoritative — and update both SRS and SDD to reflect it consistently.
- Expected benefit: Clear scope control and reliable traceability from requirements to implementation.
