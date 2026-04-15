# TVPSS-MAIN Architecture Issues

## Working Notes
- Findings will be added here during route/controller/model/view structure review.

## Findings

### 1. Authorization depends on scattered controller logic instead of a stable boundary
- Impact: High
- Why it is architectural: Security and module access are not enforced where subsystems meet; they depend on per-method query habits.
- Evidence: Shared admin route group in `routes/web.php`, disabled role middleware in `bootstrap/app.php`, and mixed scoped/unscoped record access in `SchoolAdminController` and `PPDAdminController`.
- Improvement direction: Introduce explicit role middleware plus policies/guards for school, district, and state scoped records.

### 2. School-admin feature boundaries have collapsed into a single controller
- Impact: High
- Why it is architectural: Equipment, school profile, versioning, student management, crew applications, achievements, donations, and dashboard queries now change together.
- Evidence: `SchoolAdminController.php` spans 1174 lines and owns most routes in `routes/schoolAdminRoutes.php`.
- Improvement direction: Split by bounded context and move domain rules into services.

### 3. Documentation describes clearer module boundaries than the code currently realizes
- Impact: Medium
- Why it is architectural: The SDD presents clear controller responsibilities and role-based permissions, but the implementation couples concerns and under-enforces boundaries.
- Evidence: `SDD.md` logical viewpoint and class diagram versus actual route/controller structure.
- Improvement direction: Update docs after refactoring so the described architecture matches the code structure.
