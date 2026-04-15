# TVPSS-MAIN Final Verdict — Review Summary

## Review Scope
- Target repo: `TVPSS-INFORMATION-MANAGEMENT-SYSTEM/TVPSS-MAIN`
- Review type: Final adjudication across Codex findings, Copilot findings, and Copilot cross-check of Codex
- Reviewer role: Senior software construction reviewer and technical adjudicator
- Date: 2026-04-16

## Project Snapshot
- Project name: TVPSS Management Information System
- Type: Web application (academic / school administration)
- Stack: Laravel 11, PHP 8.2, Inertia.js, React 18, Tailwind, MUI, MongoDB
- Architecture: Modular monolith — role-based route files, MVC / controller-heavy
- Role areas: Super Admin, State Admin, PPD Admin, School Admin, Student
- Domain: Malaysian school TV resource (TVPSS) lifecycle management
- Context: Academic project (UTM SECJ 2253). No vendor/node_modules present — static review only.

## Input Artifacts Reviewed
- `Reviews/Codex/software-construction-and-documentation-review.md` (primary Codex output)
- `Reviews/Codex/implementation-issues.md`
- `Reviews/Codex/architecture-issues.md`
- `Reviews/Codex/documentation-issues.md`
- `Reviews/Codex/priority-fix-plan.md`
- `Reviews/Copilot/copilot-review-1.md`
- `Reviews/Copilot-Crosscheck/codex-review-fact-check.md`
- `Software Documents/SRS.md`
- `Software Documents/SDD.md`

## Executive Verdict

This project is in a low construction maturity state with several issues that cross the line from code smell into functional contract failure. The codebase has legible intent — role-separated routes, enum-backed status modeling, FormRequest scaffolding — but that intent is consistently undermined by what was not implemented. Role middleware is disabled. Ownership is not enforced. A god controller has absorbed every school-side subsystem. The persistence layer carries undetected schema invariant breaks. The documentation amplifies rather than mitigates this: it describes a richer, more secure, and better-modeled system than the code delivers.

## Top Problems (Final Adjudicated)

1. Authorization is structurally absent at the route layer — all authenticated users can reach all admin endpoints, and the mechanism to fix this (CheckRole middleware) currently has broken redirect targets that would cause immediate failures if re-enabled.
2. The persistence layer has silent invariant failures — the achievement schema migration is broken at definition level, and the MongoDB-default + SQL-style migration combination means no foreign key constraint is ever enforced at the database layer.
3. Payment integration has plaintext secrets and a dev-environment URL hard-coded in a controller, with no adapter interface and no environment separation.
4. SchoolAdminController has collapsed eight to ten subsystems into 1,174 lines — every high-priority fix is harder because of this file.
5. The crew application workflow (the system's central student-facing feature) does not implement the documented contract from UC009/UC011/UC012 — no duplicate check, no rejection reason, no notifications, no scheduling.

## Verdict Scores
- Software construction maturity: Low
- Documentation alignment maturity: Low
- Reuse maturity: Low

## Adjudication Outcome Summary

| Finding | Source | Final Status | Priority |
|---|---|---|---|
| Role boundary non-enforcement | Both | Confirmed | High |
| CheckRole middleware has broken redirect targets | Copilot | Confirmed | High |
| SchoolAdminController god controller | Both | Confirmed | High |
| Achievement schema/invariant broken | Copilot | Confirmed | High |
| MongoDB + SQL migration strategy mismatch | Copilot | Confirmed | High |
| Payment integration hard-coded secrets | Copilot | Confirmed | High |
| Crew application workflow vs documented contract | Codex | Confirmed | High |
| SDD architecture description contradicts code | Codex | Confirmed | High |
| Student IC-only authentication | Codex | Confirmed | High |
| Status vocabulary mismatch (frontend/backend) | Codex | Confirmed | Medium |
| Equipment update redirect bug | Both | Confirmed | Medium |
| Route-model binding contract mismatch | Copilot | Confirmed | Medium |
| Duplicate route names across role files | Copilot | Confirmed | Medium |
| Duplicate follow-up logic across controllers | Copilot | Confirmed | Medium |
| Student session middleware → POST route redirect | Copilot | Confirmed | Medium |
| FormRequest validation duplicated in controllers | Copilot | Confirmed | Medium |
| SDD sequence diagrams are placeholder-only | Codex | Confirmed | Medium |
| SRS/SDD module inventory inconsistency | Codex | Confirmed | Medium |
| PWA claims unsupported in repo | Codex | Confirmed | Medium |

## Findings Not Carried Forward
- "No vendor/node_modules" — workspace constraint, not a project defect.
- Naming convention inconsistencies — valid but surface-level; merged into quick-wins.
