# TVPSS-MAIN Priority Fix Plan

## Draft
- Priority recommendations will be refined after the main review.

## Prioritized Actions

1. Reinstate and enforce role-aware access control
- Apply role middleware or policies to each route group.
- Add school/district/state ownership checks to every mutable controller action.

2. Harden the student access mechanism
- Replace IC-only login with a real authentication or one-time verified access flow.
- Add throttling and stronger session binding.

3. Repair the crew application workflow contract
- Add duplicate-application checks, structured statuses, rejection reasons, and notification hooks.
- Decide whether interview scheduling and acceptance artifacts are in scope; then implement or de-scope them in the SRS.

4. Refactor the school-admin backend into module-oriented controllers/services
- Extract equipment, school profile, versioning, students, crew approvals, achievements, and donations into separate units.
- Move TVPSS version rule calculation into a dedicated service with tests.

5. Clean up documentation drift
- Normalize the official module list across SRS and SDD.
- Remove unsupported PWA claims or add the missing platform artifacts.
- Restore or re-export usable sequence diagrams into the repository.

## Quick Wins
- Fix `equipmentUpdate()` redirect to include the required route parameter.
- Unify crew-application status constants between backend and frontend.
- Replace the stock Laravel README with project-specific setup and architecture notes.

## Validation Note
- Current workspace snapshot does not contain `vendor/` or `node_modules/`, so implementation verification in this review relied on static inspection rather than executing tests or the frontend build.
