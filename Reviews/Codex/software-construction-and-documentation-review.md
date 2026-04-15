# Software Construction and Documentation Review

Static review only. `vendor/` and `node_modules/` are absent in this workspace snapshot, so this review is based on source/document inspection rather than executing the app or tests.

## 1. Top 5 Most Important Problems
1. Role and tenant boundaries are not enforced consistently: all admin route files sit behind shared `auth`/`verified` middleware, while several controllers still mutate records by raw ID.
2. Student authentication is only an IC-number lookup plus session write, which is a weak identity contract for a workflow that exposes student application data.
3. The documented crew-application workflow is materially richer than the implementation: duplicate prevention, rejection reasons, notifications, scheduling, and detailed result handling are mostly absent.
4. `SchoolAdminController` has collapsed multiple subsystems into one 1174-line controller, which is now the main architecture bottleneck.
5. The documents drift from each other and from the code: module lists are inconsistent, PWA claims are unsupported in the repo, and the SDD sequence-diagram section is not actually reviewable.

## 2. Implementation Issues

### Frontend Issues
- Title: Student application result page uses inconsistent status vocabulary
- Major Category: Implementation/Frontend
- Secondary Lens: Contract/Postcondition
- Location: `resources/js/Pages/5-Students/ResultApply.jsx:123-129,236-270`; `app/Http/Controllers/StudentController.php:76-80`; `app/Http/Controllers/SchoolAdminController.php:924-939`
- Problem: badges recognize `Approved` and `Permohonan Belum Diproses`, but the modal logic checks `Diluluskan` and `Dalam Proses`.
- Why it matters: approved and pending applications can be rendered with the wrong headline and wrong CTA, so the UI contradicts the actual stored state.
- Evidence: backend writes `Permohonan Belum Diproses`, `Approved`, and `Rejected`; the modal branches on different strings.
- Severity: Medium
- Recommendation: define one canonical crew-application status enum/constants set and reuse it in both PHP and React.
- Expected benefit: correct student-facing behavior and less brittle UI logic.

### Backend Issues
- Title: Route-level role protection is missing and ownership checks are incomplete
- Major Category: Implementation/Backend
- Secondary Lens: Architecture/Boundary; Defensive Programming
- Location: `routes/web.php:31-46`; `bootstrap/app.php:14-18`; `app/Http/Controllers/SchoolAdminController.php:244-313,918-952`; `app/Http/Controllers/PPDAdminController.php:162-205,278-282`
- Problem: admin routes are grouped only by `auth`/`verified`; role middleware is disabled; several mutations read records with `findOrFail()` and no school/district constraint.
- Why it matters: access control depends on scattered controller habits instead of a stable server-side boundary, creating cross-role and cross-tenant exposure risk.
- Evidence: `CheckRole` is commented out; `saveFollowUp()`, `getFollowUps()`, `editStudcrew()`, `approveStudcrew()`, `rejectStudcrew()`, and PPD equipment mutation methods all operate on global IDs.
- Severity: High
- Recommendation: apply role middleware/policies to each route group and require school/district/state scoping before every mutation.
- Expected benefit: restores trust in permissions and reduces security regressions.

- Title: Student login is only an IC-number lookup
- Major Category: Implementation/Backend
- Secondary Lens: Contract/Precondition; Defensive Programming
- Location: `app/Http/Controllers/StudentController.php:19-31`; `routes/studentRoutes.php:9-13`; `app/Http/Middleware/StudentSessionCheck.php:13-20`
- Problem: the student “login” flow accepts only `ic_num`, loads the first match, and stores it in session.
- Why it matters: anyone who knows or guesses an IC can impersonate a student and access crew-application data.
- Evidence: no password, token, OTP, throttling, or second factor exists in the student path.
- Severity: High
- Recommendation: replace IC-only login with real authentication or a verified one-time access flow, plus throttling.
- Expected benefit: protects student identity and makes the student subsystem defensible.

- Title: `SchoolAdminController` is a god controller
- Major Category: Implementation/Backend
- Secondary Lens: Architecture/Boundary; Maintainability/Evolvability
- Location: `app/Http/Controllers/SchoolAdminController.php:27-1143`; `routes/schoolAdminRoutes.php:7-79`
- Problem: one controller owns equipment, locations, school profile, TVPSS version logic, students, crew approval, achievements, donations, and dashboard queries.
- Why it matters: unrelated changes amplify each other, testing is harder, and subsystem reuse is poor.
- Evidence: the controller spans 1174 lines and contains both CRUD endpoints and inline domain rules such as `checkTVPSSVersion()`.
- Severity: High
- Recommendation: split by module/bounded context and move version/approval rules into dedicated services.
- Expected benefit: smaller change surfaces, clearer ownership, easier tests, and better modularity.

- Title: Equipment update success path can fail on redirect
- Major Category: Implementation/Backend
- Secondary Lens: Exception Contract
- Location: `app/Http/Controllers/SchoolAdminController.php:204-241`; `routes/schoolAdminRoutes.php:16-17`
- Problem: `equipmentUpdate()` redirects to `route('equipment.edit')` without the required `{equipment}` parameter.
- Why it matters: a nominally successful update can end in a routing exception instead of the promised success flow.
- Evidence: route definition requires `/equipment/{equipment}/edit`; controller omits the parameter.
- Severity: Medium
- Recommendation: redirect with the current equipment ID or back to the equipment list.
- Expected benefit: preserves the intended postcondition after updates.

## 3. Documentation Issues

### Diagram / Flow Discrepancies
- Title: SDD sequence-diagram section is not reviewable as stored in the repo
- Major Category: Documentation/Diagram Discrepancy
- Secondary Lens: Maintainability/Evolvability
- Location: `Software Documents/SDD.md:1969-2049`
- Problem: the section is mostly repeated figure labels such as `Figure 4.4`, without the actual sequence content preserved.
- Why it matters: the repo cannot support the documented claim that interaction flows are specified and reviewable.
- Evidence: no corresponding diagram assets are present under `Software Documents`, and the Markdown section contains repeated caption placeholders.
- Severity: Medium
- Recommendation: re-export the real diagrams into the repo or replace the placeholders with textual sequence descriptions.
- Expected benefit: makes interaction design reviewable and maintainable.

### Missing Use Cases
- Title: Donation and equipment-report capabilities are in code/SDD but not stably represented in the SRS scope/features
- Major Category: Documentation/Missing Use Case
- Secondary Lens: Subsystem Reuse; Architecture/Boundary
- Location: `Software Documents/SRS.md:170-178,1042-2440`; `Software Documents/SDD.md:181-190`; `routes/donationRoutes.php`; `routes/ppdAdminRoutes.php`
- Problem: the SRS scope names four modules, while the code and SDD include donation and equipment-report behavior.
- Why it matters: subsystem boundaries are not stable across artifacts, so future work has no single trustworthy requirements baseline.
- Evidence: SRS scope lists four modules only; SDD says “four main modules” but lists six; code has donation routes and PPD equipment-management routes.
- Severity: Medium
- Recommendation: reconcile the official module/use-case inventory across SRS, SDD, and the repo.
- Expected benefit: clearer scope control and better traceability.

### Use Case Mismatches
- Title: Crew application workflow does not implement the documented contract
- Major Category: Documentation/Use Case Mismatch
- Secondary Lens: Contract/Postcondition; Maintainability/Evolvability
- Location: `Software Documents/SRS.md:1386-1473,1585-1747`; `app/Http/Controllers/StudentController.php:61-118`; `app/Http/Controllers/SchoolAdminController.php:924-939`; `resources/js/Pages/5-Students/ApplyCrew.jsx`; `resources/js/Pages/5-Students/ResultApply.jsx`; `resources/js/Pages/4-SchoolAdmin/StudentManagement/approveStudCrew.jsx`
- Problem: UC009/UC011/UC012 document duplicate prevention, rejection reasons, notifications, scheduling, acceptance details, and feedback, but the implementation mostly stores a status string and renders basic views.
- Why it matters: maintainers cannot trust the use cases as implementation contracts, and users get a thinner flow than the documents promise.
- Evidence: no duplicate-application check in `applyCrewSubmit()`; no rejection-reason capture in `rejectStudcrew()`; no notification/scheduling code; result UI shows no evaluator feedback or acceptance artifact.
- Severity: High
- Recommendation: either implement the documented alternate/exception flows and postconditions, or reduce the SRS to match delivered behavior.
- Expected benefit: restores requirements traceability and reduces feature ambiguity.

### Architecture Documentation Issues
- Title: SDD claims stronger role boundaries and cleaner subsystem ownership than the code provides
- Major Category: Documentation/Architecture Issue
- Secondary Lens: Architecture/Boundary
- Location: `Software Documents/SDD.md:1415-1433,1818-1847,2055-2069`; `routes/web.php:31-46`; `bootstrap/app.php:14-18`; `routes/schoolAdminRoutes.php:7-79`; `app/Http/Controllers/SchoolAdminController.php:27-1143`
- Problem: the SDD describes role-based permissions and modular subsystem/controller ownership, but the code shares admin routes under one auth group and concentrates most school-admin behavior in one controller.
- Why it matters: the architecture description is optimistic rather than descriptive, which misleads future design and review work.
- Evidence: SDD says users only access permitted areas and presents subsystem organization; implementation disables role middleware and routes most school-admin features through `SchoolAdminController`.
- Severity: High
- Recommendation: update the architecture docs after refactoring or revise them now to reflect the current code truthfully.
- Expected benefit: reduces documentation drift and bad architectural assumptions.

## 4. Reuse Review
- Application System Reuse: Low. The system is tightly coupled to a Laravel/Inertia web deployment and the repo does not contain the PWA artifacts claimed in the docs.
- Subsystem Reuse: Low. Boundaries are weak, especially in the school-admin area where many subsystems change through one controller.
- Module/Object Reuse: Low to Moderate. Eloquent models and enums are somewhat reusable, but controller logic is highly role- and route-specific.
- Function Reuse: Low. Status handling, scoping logic, and file-upload patterns are repeated instead of centralized.

## 5. Contract and Defensive Programming Review
- Preconditions are weak around identity and role: student access is IC-only, and admin role checks are not enforced at route boundaries.
- Postconditions are weak in several flows: equipment update can redirect incorrectly, and the documented crew-flow postconditions are not met.
- Invariants are underprotected: one pending crew application per student, canonical status vocabulary, and tenant ownership are not enforced consistently.
- Exception behavior is inconsistent: the code mixes `abort(403)`, redirects, JSON errors, and placeholder/error-prone routes such as `some.error.page` in `StateAdminController::generateCertificate()`.
- Assertions and regression protection are minimal: the test suite is mostly framework scaffold tests and does not cover the domain flows reviewed here.

## 6. Architecture and Modular Design Smells
- Layer leakage: controllers contain domain rules, persistence logic, UI orchestration, and file handling together.
- Tight coupling: route files, controllers, and role-specific React pages are strongly tied to each other.
- Duplicated responsibilities: access-control and status semantics are redefined in multiple places.
- God module: `SchoolAdminController` is the dominant design smell.
- Implicit contracts: school/district ownership is assumed rather than enforced systematically.
- Documentation/code drift: SRS, SDD, and implementation do not describe the same module and access model.

## 7. Quick Wins
- Fix `equipmentUpdate()` to redirect with the required equipment parameter.
- Unify crew-application status constants across backend and frontend.
- Add ownership checks to `saveFollowUp()`, `getFollowUps()`, and studcrew approve/reject/delete actions.
- Replace the stock Laravel README with project-specific setup, module, and architecture notes.
- Correct obviously wrong counters such as `StateAdminController::getStateAdminStats()` using `Pending` for an “approved” count.

## 8. Long-Term Improvements
- Introduce route-level role middleware and model policies for school/district/state scoping.
- Split school-admin behavior into module-oriented controllers and services.
- Make crew application a proper bounded workflow with statuses, reasons, notifications, and scheduling decisions modeled explicitly.
- Reconcile SRS and SDD into one stable subsystem map and regenerate usable diagrams into the repo.
- Add feature tests for role access, crew workflow, and TVPSS version approval.

## 9. Strengths Found
- The project already uses enum-backed modeling in `TVPSSVersion`, which is a good base for stricter status/version contracts.
- User and equipment flows partially use dedicated request validation classes instead of putting all validation inline.
- Some school-scoped queries do exist in list/edit flows, which shows the intended tenancy model even though it is not applied consistently.

## 10. Obsidian Notes Created/Updated
- `TVPSS-MAIN Review/review-summary.md`
- `TVPSS-MAIN Review/implementation-issues.md`
- `TVPSS-MAIN Review/documentation-issues.md`
- `TVPSS-MAIN Review/architecture-issues.md`
- `TVPSS-MAIN Review/priority-fix-plan.md`
- `TVPSS-MAIN Review/software-construction-and-documentation-review.md`

## 11. Final Verdict
- Software construction maturity: Low
- Documentation alignment maturity: Low
- Current reuse maturity: Low
- Most reusable part of the project: the enum-backed domain model pieces around TVPSS version/status handling
- Least reusable part of the project: the school-admin controller/route/page cluster
- Biggest blocker to maintainability: collapsed subsystem boundaries in `SchoolAdminController`
- Biggest blocker to reuse: hardcoded role and tenant assumptions in controller logic
- Biggest documentation risk: SRS/SDD promise workflows and architecture boundaries that the code does not actually implement
- Biggest architecture/construction risk: access control is not enforced as a first-class boundary
