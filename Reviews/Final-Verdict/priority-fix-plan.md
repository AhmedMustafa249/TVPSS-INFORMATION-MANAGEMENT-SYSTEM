# TVPSS-MAIN Final Verdict — Priority Fix Plan

## Basis
This plan is derived from the final adjudication of Codex findings, Copilot findings, and the Copilot cross-check of Codex. Issues are sequenced by dependency and impact. Items in Phase 1 must be resolved before Phase 2 actions are safe to execute.

---

## Phase 1 — Critical Blockers (fix before anything else)

### 1. Fix CheckRole middleware redirect targets before re-enabling
- Why first: The `CheckRole` middleware redirects to route names that do not exist. Re-enabling it without this fix will cause immediate route-resolution failures across all admin paths. This is the hidden dependency that makes the obvious first step (enable role enforcement) actively dangerous.
- Action: Audit all redirect targets inside `CheckRole`. Replace every undefined route name with a valid named route. Verify by running `php artisan route:list` and confirming each target exists.

### 2. Clarify and commit to one persistence strategy (MongoDB or SQL)
- Why second: The entire persistence correctness analysis depends on knowing which FK constraints, if any, the database actually enforces. All schema-level fixes (including the achievement migration) are shaped by this decision.
- Action: If MongoDB remains the default, remove all SQL-style `->foreignId()`, `->constrained()`, and `->references()->on()` calls from migrations. Replace with application-level validation and document-embedding or reference patterns appropriate for MongoDB. If switching to SQL, change `config/database.php` default, run migrations against a relational DB, and verify.

---

## Phase 2 — High Priority (security, data integrity, core contract)

### 3. Enforce role and tenant boundaries at the routing layer
- Action: Apply role middleware or policies per route group. Require school/district/state scoping in all mutating controller actions via query scopes or model policies.
- Depends on: Phase 1 item 1 (CheckRole must be safe to re-enable first).

### 4. Fix achievement persistence invariant
- Action: Choose one identity strategy for `student_achievements`. If domain codes are needed, add `achievement_code` as a separate column alongside a numeric PK. Define `student_id` column before the FK constraint. Update the controller to write to the correct columns.
- Depends on: Phase 1 item 2 (persistence strategy must be decided first).

### 5. Externalize payment credentials and add an adapter boundary
- Action: Move `userSecretKey`, `categoryCode`, and the provider URL to `.env` / `config/services.php`. Wrap the provider call behind a `PaymentGatewayInterface`.
- Why: Plaintext secrets in source and a dev endpoint in production-path code are active deployment risks.

### 6. Repair or descope the crew application workflow contract
- Action: Either implement the missing behaviors from UC009/UC011/UC012 — duplicate-application check in `applyCrewSubmit()`, rejection-reason field in `rejectStudcrew()`, notification hooks, result artifacts — or formally reduce the SRS use cases to match delivered behavior. Do not leave the gap unacknowledged.

### 7. Harden student authentication
- Action: Replace IC-only session with real authentication (password, OTP, or verified one-time link) plus request throttling and session-bound identity.

---

## Phase 3 — Medium Priority (architecture, maintainability, contracts)

### 8. Decompose SchoolAdminController by bounded context
- Action: Extract into `EquipmentController`, `SchoolProfileController`, `TVPSSVersionController`, `StudentAdminController`, `AchievementController`. Move `checkTVPSSVersion()` rules and crew approval logic into dedicated service classes.

### 9. Unify crew-application status vocabulary across backend and frontend
- Action: Define one canonical status constant set (PHP-backed enum or shared constants). Remove all status strings that are inconsistent between `StudentController`, `SchoolAdminController`, and `ResultApply.jsx`.

### 10. Fix route contract mismatches
- Action: Standardize route parameter names so typed model binding works correctly (`{equipment}` not `{id}`). Add the missing parameter to the `equipmentUpdate()` redirect. Namespace route names per subsystem (`ppd.schoolInfo.*`, `state.schoolInfo.*`) to eliminate collision between PPD and State route files.

### 11. Fix student session middleware redirect target
- Action: Change `StudentSessionCheck` redirect from `student.login` (POST) to `student.showLogin` (GET).

### 12. Extract shared follow-up creation logic
- Action: Create a `CreateEquipmentFollowUpAction` service class. Both `SchoolAdminController::saveFollowUp()` and `PPDAdminController::saveFollowUp()` invoke the shared action with role-specific authorization injected.

### 13. Remove duplicate validation from FormRequest-backed controllers
- Action: Remove inline `$request->validate(...)` calls from `UserController::store()` and `update()`. Ensure `authorize()` is implemented in each FormRequest class.

---

## Phase 4 — Documentation Reconciliation

### 14. Reconcile the official module inventory
- Action: Produce a single authoritative module list — the six modules reflected in the code — and update both SRS and SDD to match. Resolve the four-vs-six discrepancy.

### 15. Add use cases for donation and equipment reporting
- Action: Either add SRS use cases (with alternate and exception flows) for donation management and PPD equipment reporting, or formally mark them out of scope and remove the associated SDD claims.

### 16. Update SDD architecture description to reflect actual code structure
- Action: After Phase 3 refactoring, update the SDD subsystem/controller mapping, role enforcement description, and logical viewpoint to match the refactored code. If refactoring is deferred, annotate the SDD to explicitly distinguish intended design from current implementation state.

### 17. Restore or replace the SDD sequence-diagram section
- Action: Re-export sequence diagrams as image files into `Software Documents/` with Markdown references, or replace the `Figure 4.x` placeholders with textual sequence descriptions.

### 18. Remove or implement PWA claims
- Action: Either add a web app manifest, service worker, and HTTPS meta, or remove PWA references from SRS and SDD.

---

## Quick Wins (can be done independently at any time)

- Fix `equipmentUpdate()` redirect to include the required `{equipment}` parameter.
- Fix student session middleware redirect to `student.showLogin`.
- Remove inline `$request->validate()` from `UserController` methods.
- Namespace conflicting route names (`ppd.schoolInfo.*`, `state.schoolInfo.*`).
- Replace the stock Laravel README in `TVPSS-MAIN/README.md` with project-specific setup, module, and architecture notes.

---

## Validation Note
The current repository snapshot does not include `vendor/` or `node_modules/`. All findings in this plan are based on static code and document inspection. Implementation verification requires running migrations, executing the test suite, and testing role-boundary behavior with live session state.
