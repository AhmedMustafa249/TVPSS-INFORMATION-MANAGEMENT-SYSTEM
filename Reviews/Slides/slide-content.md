# TVPSS MIS — Software Construction Review
## Slide Deck Content

Team: The Sprint Squad
Status: Content finalized — pending frontend build

---

## Slide 1 — Title / Intro

**Title:** TVPSS Management Information System
**Subtitle:** Software Construction Review — Findings & Analysis
**Team:** The Sprint Squad

| # | Name | Matric |
|---|---|---|
| 1 | Ahmed Mustafa | A22EC9148 |
| 2 | Hanan Osama | A22EC4042 |
| 3 | Mustafa Tarig | A22EC0022 |
| 4 | Raghad Zeinalabdin | A22EC9002 |
| 5 | Wang Ya Peng | ________ |

---

## Slide 2 — Agenda

**Title:** What This Deck Covers

- System overview
- How we reviewed it
- Overall verdict
- Issues found — grouped by category
- Priority fix plan

---

## Slide 3 — System Overview

**Title:** The System Being Reviewed

- **What it is:** A web-based management system for Malaysian school TV resources (TVPSS)
- **Stack:** Laravel 11 · PHP 8.2 · Inertia.js · React 18 · MongoDB
- **Roles:** Super Admin · State Admin · PPD Admin · School Admin · Student
- **Modules:** Dashboard, School Info, TVPSS Versioning, Student Achievement, Donation, Equipment Reporting

---

## Slide 4 — Review Methodology

**Title:** How We Reviewed the System

Three layers of analysis:

1. **Static code review** · source code inspection across all controllers, routes, middleware, and models
2. **Documentation review** · SRS and SDD compared against actual implementation
3. **Cross-checking** · each team member's findings were reviewed and challenged by other members before being accepted
4. **Runtime testing** · the application was run live and failures observed directly

> All findings in this deck are confirmed — either by multiple team members or by direct observation during live testing.

---

## Slide 5 — Overall Verdict

**Title:** The Bottom Line

| Dimension | Rating |
|---|---|
| Software Construction Maturity | 🔴 Low |
| Documentation Alignment Maturity | 🔴 Low |
| Reuse Maturity | 🔴 Low |

**Three biggest risks:**
- Authorization is structurally absent — any logged-in user can reach any admin endpoint
- The persistence layer has silent invariant failures the database never surfaces
- The SDD describes an architecture that does not exist in the code

---

## Slide 6 — Issue Cluster: Security & Authorization

**Title:** Security — The Structural Gap

**3 confirmed High-severity findings:**

- **B-1 · No role enforcement at routing layer**
  All admin roles share one auth group. Role middleware (`CheckRole`) is disabled.

- **B-1 (blocker) · Dead middleware redirect targets**
  Re-enabling `CheckRole` would immediately crash the system — it redirects to route names that don't exist.

- **B-5 · Student authentication is IC-number only**
  No password, no token, no throttling. Anyone who knows a student's IC number has full access.

- **B-10 · Student login page exists but backend support is missing**
  No student role in middleware. No student records in database seeders. The login flow cannot succeed in any fresh deployment.

---

## Slide 7 — Issue Cluster: Data Integrity

**Title:** Data Layer — Silent Failures

**3 confirmed High-severity findings:**

- **B-3 · MongoDB default + SQL-style migrations**
  Every foreign key constraint in every migration file is silently ignored — MongoDB never processes them. The schema documentation is fiction.

- **B-2 · Achievement schema invariant is broken**
  Migration defines a numeric ID column. Controller writes string IDs (`PS0001`). A foreign key references a column that was never defined. The migration cannot run correctly — and MongoDB hides it.

- **B-4 · Payment credentials are hard-coded in a controller**
  Secret key, category code, and a dev-environment URL (`https://dev.toyyibpay.com`) are literal strings inside `paymentController.php`. No environment separation. No adapter interface.

---

## Slide 8 — Issue Cluster: Maintainability

**Title:** Architecture — The Maintainability Bottleneck

**The core problem:** `SchoolAdminController` — 1,174 lines, 40+ methods, 8–10 distinct subsystems in one file.

Everything it owns: Equipment · Follow-ups · Locations · School Profile · TVPSS Versioning · Students · Crew Approval · Achievements · Donations · Dashboard Statistics

**Why it matters:** Every high-priority fix touches this file. Change amplification is unavoidable.

**Supporting findings:**
- **B-6** · Duplicate follow-up workflow logic in `SchoolAdmin` and `PPDAdmin` controllers
- **B-7** · Route parameter naming inconsistencies cause 404/500 failures on specific paths
- **B-8** · FormRequest validation duplicated inside controllers that already declare it

---

## Slide 9 — Issue Cluster: Runtime Failures

**Title:** Broken at Runtime — Confirmed by Live Testing

Features that are visible in the UI but do not function:

| Finding | What Fails |
|---|---|
| **F-4** | Role management button — renders, does nothing |
| **F-5** | Document preview — blank or error, no feedback to user |
| **F-6** | Calendar view toggles — Daily / Weekly / Monthly buttons have no effect |
| **B-10** | Student login — page renders, login cannot succeed (no seeder data) |

> These were all observed directly by running the application.

---

## Slide 10 — Issue Cluster: Frontend UX

**Title:** Frontend — UX and Contract Failures

- **F-1 · Status vocabulary mismatch**
  Backend writes `Approved` / `Permohonan Belum Diproses`. The result page modal checks `Diluluskan` / `Dalam Proses`. An approved student sees the wrong message.

- **F-2 · Card layout overlapping**
  Card elements overlap each other. Fragile layout — breaks on varying content or screen size.

- **F-3 · Navigation arrows missing from dashboard**
  Present on landing and login pages. Absent from dashboard. UI convention established and then abandoned.

---

## Slide 11 — Issue Cluster: Documentation Gaps

**Title:** Documentation — Promising More Than Was Built

- **D-4 · Crew application workflow not implemented**
  UC009/UC011/UC012 specify: duplicate prevention · rejection reasons · notifications · scheduling · acceptance artifacts. Implementation: a status string and basic views.

- **D-5 · SDD describes an architecture that doesn't exist**
  SDD claims role-enforced modular subsystems. Reality: role middleware disabled, one controller for 8–10 subsystems.

- **D-6 · SRS and SDD disagree on module count**
  SRS: 4 modules. SDD: claims 4, lists 6. Code: implements 6. No single document is correct.

- **D-2/D-3 · Missing use cases + unsupported PWA claim**
  Donation and equipment-report modules have no SRS use cases. PWA described in both documents — no service worker, no manifest exists in the repo.

---

## Slide 12 — Root Cause Themes

**Title:** Why These Issues Exist — The Deeper Patterns

1. **Framework-led design** — Laravel's structure defined the architecture instead of the architecture defining how Laravel was used
2. **Authorization by intent, not mechanism** — Role boundaries were designed but never operationalized as enforced boundaries
3. **Documentation written in isolation** — SRS and SDD were produced by separate teams, never reconciled against the final code
4. **Persistence strategy ambiguity** — MongoDB runtime, SQL migration semantics, no explicit commitment to either
5. **God-module concentration** — Unconstrained feature accumulation in one controller, compounding every other problem

---

## Slide 13 — Priority Fix Plan

**Title:** What Should Be Fixed First

**Phase 1 — Must do before anything else:**
- Fix `CheckRole` redirect targets (broken path blocks all authorization work)
- Decide: MongoDB or SQL? Remove the contradicting artifacts

**Phase 2 — High priority:**
- Enforce role + tenant boundaries at routing layer
- Fix achievement schema and controller ID strategy
- Externalize payment credentials
- Implement or descope the crew application workflow
- Fix student seeder data and role definition

**Phase 3 — Medium priority:**
- Decompose `SchoolAdminController` by bounded context
- Fix broken UI: document preview, calendar toggles, role button
- Fix route parameter mismatches, route name collisions
- Unify status vocabulary across backend and frontend

**Phase 4 — Documentation:**
- Reconcile SRS/SDD module inventory
- Update SDD to reflect real code architecture
- Add use cases for donation and equipment-report modules

---

## Slide 14 — Closing / Final Verdict

**Title:** Final Verdict

> The system has the right intent but not the right implementation. Role separation is named but not enforced. Documentation is detailed but not accurate. The student flow is designed but not deployable. The foundation needs to be corrected before features can be safely extended.

**The single most important issue:** Authorization is absent as a structural boundary — and the path to fixing it is currently broken.

**The single most important strength:** The architectural intent is sound. Role-based route files, enums, FormRequest scaffolding, and Inertia separation are all good starting points. The work is refinement, not a rewrite.
