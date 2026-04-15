# Speaker Notes — TVPSS MIS Software Construction Review
## The Sprint Squad

---

### Slide 1 — Title

- Introduce the team briefly. We're The Sprint Squad — five members who jointly reviewed the TVPSS Management Information System.
- TVPSS = Televisyen Pusat Sumber Sekolah. It's a Laravel + React web app for managing school TV resources in Malaysian schools.
- Our review had four layers: static code inspection, documentation review, team cross-checks, and live runtime testing.
- Every finding you'll see was either verified by more than one team member or directly observed by running the app.

---

### Slide 2 — Agenda

- Quick roadmap: context first, then how we worked, then the verdict, then six clusters of issues, then what to fix and in what order.
- The order of the issue slides isn't random — we go from most critical to least critical.

---

### Slide 3 — System Overview

- Key things to anchor the audience on before we get into issues:
- It uses MongoDB — this becomes critical when we talk about data integrity. SQL-style foreign keys don't actually do anything on MongoDB.
- Five role types means access control is architecturally important — which is exactly where one of the biggest failures is.
- Six modules exist in code, but the SRS only documents four. That mismatch is itself a finding.

---

### Slide 4 — Methodology

- We want to be clear that these aren't opinions — they're confirmed findings.
- Static review: we read controllers, routes, middleware, models, migrations, and matched them against the SRS and SDD.
- Cross-checking: before any finding made it into the final report, at least one other team member had to verify or challenge it. Weak findings got dropped.
- Runtime testing: we ran the app. Some things that look fine in code are broken at runtime — and we caught several of those.

---

### Slide 5 — Overall Verdict

- All three maturity scores are Low. That's the honest summary.
- The three risks we're highlighting aren't style complaints — they're structural failures.
- First: authorization literally does not exist at the routing layer right now. Any logged-in user can hit any admin endpoint.
- Second: the database never enforces any foreign key constraint — MongoDB silently ignores all of them. Migrations say one thing, the database does another.
- Third: the SDD describes a modular, role-enforced architecture. The code has neither. Anyone reading the SDD to make design decisions is working from a false map.

---

### Slide 6 — Security & Authorization

- This is the single most critical cluster.
- B-1: `CheckRole` middleware is commented out in `bootstrap/app.php`. It's not missing — it was written and then disabled. So there is zero role enforcement at runtime.
- The blocker is important to explain: if you try to fix this by just re-enabling `CheckRole`, the system immediately crashes — because the middleware redirects to route names that don't exist. The fix path itself is broken.
- B-10: the student login page renders perfectly. But there's no student role defined in the middleware, and no student records in the database seeders. In any fresh install, the login flow is a dead end.

---

### Slide 7 — Data Layer

- Silent failures are the most dangerous kind — they don't throw errors, they just quietly corrupt.
- B-3: every migration file uses SQL-style foreign key declarations. MongoDB ignores all of them. So the schema documentation describes constraints that the database never enforces.
- B-2: the achievement migration creates a numeric auto-increment ID column. The controller then writes string IDs like `PS0001` to it. And a foreign key references a column that was never defined. None of this throws an error because MongoDB is schema-flexible — it just silently accepts whatever you write.
- B-4: literal string `https://dev.toyyibpay.com` is in the payment controller. That's the dev URL, in production code. The secret key is also hardcoded — no environment variable, no config file.

---

### Slide 8 — Maintainability

- One class. 1,174 lines. Over 40 public methods. Ten distinct, unrelated domains.
- The pill badges show everything this one controller owns. Equipment, versioning, students, achievements, donations — it's all in one file.
- This is the architectural bottleneck. Every high-priority fix we identified in this deck requires navigating this file. There's no way to test or change any one domain without risk of affecting the others.
- B-6 and B-7 are direct symptoms of this concentration — logic gets duplicated because there's no shared service layer.

---

### Slide 9 — Runtime Failures

- These weren't found from reading code. We ran the app.
- F-4: a button in the role management area renders and looks clickable. Nothing happens when you click it.
- F-5: the document preview area either stays blank or throws an error. No message to the user.
- F-6: the calendar has Daily, Weekly, and Monthly view buttons. All three are non-functional — the state switch is disconnected from the rendering.
- B-10 shows up here again because it's also a runtime failure: the student login page is a complete dead end in any fresh installation.

---

### Slide 10 — Frontend UX

- F-1 is subtle but real: the backend writes `Approved` and `Permohonan Belum Diproses`. The result page modal checks for `Diluluskan` and `Dalam Proses`. Those two strings are never written by the backend. So an approved student sees the right badge color but wrong modal text and wrong CTA.
- F-2: card elements overlap each other visually — fragile layout that breaks on different content lengths or screen sizes.
- F-3: navigation arrows are on the landing page and login page, but not the dashboard. The component wasn't reused — each page builds its own navigation independently.

---

### Slide 11 — Documentation Gaps

- The crew application workflow is the central student-facing feature and the most documented part of the SRS. UC009, UC011, UC012 describe duplicate prevention, rejection reasons, notifications, scheduling, and acceptance artifacts. The implementation is one status string and basic views. None of those flows were built.
- D-5: the SDD was written as a design document describing a modular, role-enforced architecture. The code was implemented differently. The SDD was never updated to match. Anyone using it as a reference is looking at a false picture.
- Module count: SRS says 4, SDD claims 4 but lists 6, code has 6. No single document is authoritative.
- PWA: both SRS and SDD say the system is a Progressive Web App. There is no service worker or manifest in the repository.

---

### Slide 12 — Root Cause Themes

- These five patterns explain why the issues exist — not just what the issues are.
- Framework-led design: Laravel gave them a structure, they followed it. The architecture was never explicitly designed — it emerged from convenience.
- Authorization by intent: the role file names, the middleware code, the route separation — the intent is there. The enforcement never was.
- Documentation isolation: SRS and SDD were written by separate teams at separate times and never reconciled with the final code.
- Persistence ambiguity: no one made an explicit decision about whether SQL semantics or MongoDB document semantics apply. Both exist simultaneously. Neither is fully right.
- God-module: SchoolAdminController is the single biggest structural obstacle. It blocks modularization, testing, and every fix that touches school-admin features.

---

### Slide 13 — Priority Fix Plan

- The phases are sequenced by dependency, not just severity.
- Phase 1 has to come first. You cannot safely re-enable `CheckRole` until its redirect targets are fixed. You cannot fix schema issues until you know which database semantics you're committing to.
- Phase 2 is the high-impact security and data work. After Phase 1, this is where the most value is.
- Phase 3 is architecture and UI — decomposing the god controller and fixing the broken buttons.
- Phase 4 is docs reconciliation — should happen after the code is fixed, not before, so the docs reflect reality.

---

### Slide 14 — Closing

- The core message: the system has the right intent. Role-based route files, enums, FormRequest classes, Inertia separation — these are all good choices. The bones are sound.
- What went wrong is enforcement and reconciliation. The role model was named but never activated. The documentation was written but never synced.
- This is refinement work, not a rewrite. But the refinement has to start from the right place: fixing the authorization path first, deciding on the persistence strategy, and then decomposing the god controller.
- Thank the audience, open for questions.
