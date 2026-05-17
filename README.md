# Software Construction — Phase 1 (Build) + Phase 2 (Handoff)

The full greenfield → maintenance cycle, built across two semester phases of **ITCS383 (Software Construction)** at the Faculty of ICT, Mahidol University.

---

## The story

**Phase 1 — built from scratch.** Our 6-person team (codename **Emerald**) designed and built [**SpaceHub**](phase-1-spacehub/), a co-working space management web app, intended to be handed off to *another* team in their Phase 2.

**Phase 2 — inherited someone else's code.** We took over **Arai-Kor-Dai**, a post-office shipping platform built by a *different* team in their Phase 1, and continued development. Before touching the code we produced a formal [**D4 Impact Analysis**](phase-2-emerald-handoff/d4-impact-analysis/), then built [**Emerald**](phase-2-emerald-handoff/android-emerald/) — the new native Android client.

This is the real-world software lifecycle: write clean code knowing someone else will inherit it, then inherit someone else's code and figure it out before changing it.

---

## Why this course matters

Most university software-engineering classes focus on **greenfield development** — blank repo, problem statement, build something. But in industry, ~80% of engineering time is spent **reading, maintaining, and extending existing code** that someone else wrote. ITCS383's two-phase format simulates exactly that:

- **Phase 1** — build a system *knowing another team will inherit it*. Forces clear naming, exhaustive documentation, test coverage, and onboarding-ready code from day one.
- **Phase 2** — inherit a system *someone else built* and continue development. Forces you to read unfamiliar code, do impact analysis, and extend without breaking what's already there.

Both halves are essential. Greenfield-only engineers write brittle code no one else can maintain. Maintenance-only engineers can't ship new things. The point of the course is to make you fluent in both directions of the lifecycle.

## Phase 1 — why SpaceHub was designed this way

| Decision | Why |
|---|---|
| **Co-working space domain** | Real domain with multiple user roles (customer / employee / manager), a revenue model, and operational complexity (equipment, expenses) — enough surface area for 6 teammates to work in parallel without constantly blocking each other. |
| **Vanilla HTML/CSS/JS frontend** (no React/Vue) | Lowered the barrier to entry so any of 6 teammates could contribute UI code without framework expertise. Trade-off accepted: less elegant code, but more contributors. |
| **PostgreSQL on Neon (serverless)** | Zero ops — no team member had to maintain a database server. Spin-up/spin-down on demand, fits a course budget. |
| **bcrypt for passwords + AES-256-GCM for PII** | Two different problems. Passwords need *one-way* hashing (can't be reversed even if the DB is stolen). PII like address needs *two-way* encryption (we need to display it back to the user). Different crypto for different reasons. |
| **Docker + Render** | Production-equivalent deployment so we'd catch infrastructure issues *during* development, not on demo day. |
| **GitHub Actions + SonarCloud** | Quality gate on every PR. "If it doesn't pass, it doesn't merge." Forces discipline that survives without a senior reviewer in the room. |
| **Writing for handoff** | Knowing our code would be inherited by another team in their Phase 2, we wrote exhaustive READMEs + the D3 AI Log + D4 Quality Report to document our decisions. |

## Phase 2 — why the handoff was hard (and what I learned)

Inheriting someone else's code is the most underappreciated software-engineering skill. You don't get to redesign from scratch — you have to **read, understand, and respect** an existing design before you change anything.

The **D4 Impact Analysis** is the formal way to do this:

1. **Map dependencies** — what does each module depend on? What depends on it? Where would a change ripple?
2. **Identify SLOs** — what does the existing system promise users (latency, availability, correctness)? You can't break those.
3. **Build a reachability matrix** — which code is reachable from each user-facing feature? If you delete this function, what breaks?
4. **Propose changes minimally** — smallest possible change that achieves the new requirement. Honor the existing API contracts.

Only **after** D4 was complete were we allowed to write new code. The **Emerald Android client** was built fresh on top of the inherited Arai-Kor-Dai backend — meaning our app design had to honor the existing API contracts (we couldn't change the server's endpoints, request shapes, or response formats; we had to design the mobile UX around what the inherited API already supported).

This is real software engineering. In some ways the D4 deliverable is more valuable than the code itself — it's the artifact that proves we understood the system before changing it.

---

## Repo structure

| Folder | What's there |
|---|---|
| [`phase-1-spacehub/`](phase-1-spacehub/) | The full SpaceHub web app I built in Phase 1 (greenfield) |
| [`phase-2-emerald-handoff/`](phase-2-emerald-handoff/) | My Phase 2 contributions: Emerald Android client + D4 Impact Analysis + traceability diagrams |

The **inherited Arai-Kor-Dai backend codebase** (built by the other team) is intentionally **not included** in this repo — only my own contributions are shown.

---

## Phase 1: SpaceHub (greenfield)

A co-working space management web app — book desks, manage members, track expenses, run reports.

| Layer | Tech |
|---|---|
| Frontend | Vanilla HTML / CSS / JavaScript |
| Backend | Node.js + Express |
| Database | PostgreSQL on Neon (serverless) |
| Security | bcryptjs (passwords) + AES-256-GCM (PII at rest), role-based access (customer / employee / manager) |
| Testing | Jest |
| Containerization | Docker |
| CI/CD | GitHub Actions + SonarCloud quality gate |
| Hosting | Render (production) |
| Team size | 6 |

→ See [`phase-1-spacehub/README.md`](phase-1-spacehub/README.md) for the full breakdown and setup instructions.

---

## Phase 2: Emerald (handoff + maintenance)

The native Android client I co-developed for the inherited Arai-Kor-Dai post-office shipping platform.

| Layer | Tech |
|---|---|
| Language | Kotlin |
| UI | Jetpack Compose + Material3 |
| Networking | Retrofit2 + Coroutines |
| Build | Gradle (Kotlin DSL) |
| Target SDK | 26–36 |
| Testing | JUnit 5 + MockK + JaCoCo coverage |
| CI | GitHub Actions + SonarCloud |
| Backend | (Inherited) Express + MySQL — not in this repo |
| Team size | 6 |

→ See [`phase-2-emerald-handoff/README.md`](phase-2-emerald-handoff/README.md) for the full breakdown and setup instructions.

---

## D4 Impact Analysis (the BA deliverable)

Before extending the inherited Arai-Kor-Dai codebase, we produced the **D4 Impact Analysis** — a Business Analysis deliverable that identified dependencies, risks, SLOs, and proposed changes against the inherited codebase. This step is what made the handoff safe.

→ Read it in [`phase-2-emerald-handoff/d4-impact-analysis/D4_IMPACT_ANALYSIS.md`](phase-2-emerald-handoff/d4-impact-analysis/D4_IMPACT_ANALYSIS.md). The connected reachability graph lives alongside it as a `.drawio` file.

---

## Author

**Rattee Watperatam** (Student ID: 6688141)
ICT, Faculty of ICT, Mahidol University
Course: **ITCS383** — Year 3 (Aug 2025 – May 2026)

[rattee.watp@gmail.com](mailto:rattee.watp@gmail.com) · [github.com/FantasticRattee](https://github.com/FantasticRattee)

## Related work

- [retail-datawarehouse-bi](https://github.com/FantasticRattee/retail-datawarehouse-bi) — Galaxy-schema data warehouse + Tableau BI for a hypothetical 50-branch 7-Eleven Thailand chain
