# TVPSS-MAIN Final Verdict — Architecture Issues

## Findings

### 1. Authorization is not enforced as an architectural boundary — and the fix path is blocked
- Impact: High
- Source: Both Codex and Copilot; expanded by cross-check
- Why it is architectural: Role and tenant enforcement is the foundational security contract of the entire system. It is not a controller-level concern — it must be enforced at the route boundary before any controller logic executes. That boundary does not currently exist.
- Evidence:
  - `routes/web.php` loads all role-specific route files (`schoolAdminRoutes.php`, `ppdAdminRoutes.php`, `stateAdminRoutes.php`, `superAdminRoutes.php`) inside one shared `auth/verified` group with no role discrimination.
  - `bootstrap/app.php` has `CheckRole` middleware commented out.
  - Multiple controller methods in `SchoolAdminController` and `PPDAdminController` use global `findOrFail($id)` without school, district, or state scoping.
  - `CheckRole` redirects to route names (`superADashControl`, etc.) not defined in any route file — re-enabling the middleware without fixing these targets causes immediate runtime failures.
- Root cause: The role middleware was created and then disabled. Authorization was delegated to per-method query habits that are applied inconsistently.
- Improvement direction:
  1. Fix `CheckRole` redirect targets to defined named routes before re-enabling.
  2. Apply role middleware or policies per route group with distinct prefixes and namespaces.
  3. Enforce school/district/state ownership in all mutating controller actions via query scopes or model policies.

### 2. MongoDB default with SQL-style migration schema produces a silent correctness gap
- Impact: High
- Source: Copilot (missed by Codex; confirmed by cross-check)
- Why it is architectural: The persistence layer strategy — what the database actually enforces versus what migration files document — determines the trustworthiness of every inter-model relationship in the system. When those two things disagree silently, every correctness analysis based on the schema is unreliable.
- Evidence:
  - `config/database.php` sets `'default' => 'mongodb'`.
  - All models extend `MongoDB\Laravel\Eloquent\Model`.
  - Migration files use `->foreignId()`, `->constrained()`, `->references()->on()` — SQL FK constructs that MongoDB never processes.
- Root cause: No explicit decision was made about which database semantics the system relies on. The MongoDB driver was adopted for its schema flexibility, but relational migration patterns were retained from a SQL-style workflow, producing documentation that describes constraints the database never enforces.
- Improvement direction: Explicitly commit to one persistence strategy. For MongoDB: remove SQL-style FK declarations and enforce inter-model constraints at the application layer. For SQL: change the default driver and run migrations against a relational DB. Do not maintain SQL FK artifacts against a MongoDB backend.

### 3. School-admin feature boundaries have collapsed into a single controller
- Impact: High
- Source: Both Codex and Copilot; confirmed by cross-check
- Why it is architectural: A module boundary is only meaningful if it constrains what can change together. When eight to ten unrelated subsystems share one controller, every change in any subsystem is coupled to every other. The controller becomes the architectural bottleneck for the entire school-admin domain.
- Evidence:
  - `SchoolAdminController.php` spans lines 27–1143 (~1,174 lines).
  - Methods span: equipment CRUD, equipment follow-ups, location management, school profile, TVPSS version calculation (`checkTVPSSVersion()` inline rules engine), student CRUD, crew approval workflow, student achievement creation, donation listing, and dashboard statistics.
  - `routes/schoolAdminRoutes.php` routes most school-admin features to this one controller.
- Root cause: No bounded context design was applied during implementation. Features were added to the nearest available controller, and the school-admin controller was the natural home for anything school-related.
- Improvement direction: Split by bounded context. Candidate controllers: `EquipmentController`, `SchoolProfileController`, `TVPSSVersionController`, `StudentAdminController`, `AchievementController`. Move domain rules (TVPSS version calculation, crew approval logic) into dedicated services with explicit inputs and outputs.

### 4. Achievement persistence invariant is broken at the migration level
- Impact: High
- Source: Copilot (missed by Codex; confirmed by cross-check)
- Why it is architectural: Schema correctness is the foundation of every data operation. A migration that defines the wrong key type and references a non-existent column is not a marginal issue — it means the persistence contract for this module was never valid.
- Evidence:
  - Migration: `$table->id()` (bigint auto-increment).
  - Controller: writes `'PS' . str_pad(count, 4, '0', STR_PAD_LEFT)` to the `id` column (string assignment to numeric PK).
  - Migration declares `$table->foreign('student_id')` without a prior column definition for `student_id`.
  - Because the database defaults to MongoDB, this schema error is invisible in normal operation — no exception is raised, but the constraint is also never enforced.
- Root cause: The achievement module was implemented without reconciling the controller's domain-code ID strategy against the migration's surrogate key definition. The MongoDB driver masked the error by not processing FK declarations.
- Improvement direction: Choose one identity strategy. Add `achievement_code` as a separate column if domain codes are needed. Define `student_id` before the FK constraint. Verify against both MongoDB and SQL environments.

### 5. Documentation describes a stronger architecture than the code realizes
- Impact: Medium-High
- Source: Codex (confirmed by both Copilot cross-check and independent Copilot review)
- Why it is architectural: Architecture documentation that is optimistic rather than descriptive misleads future design work. Decisions made on the basis of the SDD assume boundaries that do not exist and enforcement that is not present.
- Evidence:
  - SDD logical viewpoint and class diagram describe modular controllers, role-enforced access, and clear subsystem ownership.
  - Actual code: role middleware disabled, one controller for eight subsystems, all admin routes in one shared auth group.
  - SRS and SDD disagree on the module count (four vs six).
- Root cause: The SDD was written as an aspirational design specification rather than a descriptive architectural document, and it was not updated after implementation decisions diverged from the design.
- Improvement direction: After any refactoring, update the SDD to reflect actual code structure. If refactoring is not imminent, add explicit annotations to the SDD marking intended design versus current implementation state. Reconcile the module inventory across SRS and SDD.

## Root Cause Themes

### Theme 1: Framework-led structure without enforced architectural discipline
The route/controller pattern is framework-imposed. The project correctly used Laravel scaffolding (route files, middleware, FormRequest, enums) but let the framework define the architecture rather than using the framework to implement a defined architecture. Features land in the nearest controller, routes go into the nearest file, and every boundary is implicit rather than enforced.

### Theme 2: Authorization designed as intent, never operationalized as mechanism
Role middleware was written, registered, and disabled. Scoped queries were written for some paths but not others. The intent of a role-enforced system exists throughout the codebase — in route file names, in controller naming conventions, in the commented-out middleware — but was never operationalized as a consistent, tested, structural boundary.

### Theme 3: Persistence strategy ambiguity
MongoDB is the runtime database, but SQL relational semantics are expressed in migrations. No explicit decision exists about which capabilities of MongoDB are being used and which migration constructs are decorative. This ambiguity means no one can confidently answer: what does the database actually enforce?

### Theme 4: Documentation drift from the start of implementation
The SRS was written by one team sprint, the SDD by another, and neither was reconciled against the final code. Both documents describe a system that was partially designed but not fully implemented. The drift is not a result of requirements changing — it is a result of documentation and implementation being conducted in isolation.

### Theme 5: God-module concentration as a change amplifier
The collapse of eight subsystems into `SchoolAdminController` is both a symptom of Theme 1 and a compounding cause of future maintainability decay. Every high-priority fix — authorization scoping, crew workflow contracts, achievement persistence — requires navigating this file.
