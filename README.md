# Software Construction — Phase 1 (Build) + Phase 2 (Handoff)

The full greenfield → maintenance cycle, built across the two phases of one course, **ITCS383 (Software Construction)**, at the Faculty of ICT, Mahidol University (Jan – May 2026).

> **Names used here.** **Emerald** is my team's name, and also the name of the Android app we built in Phase 2. **SpaceHub** is the project we built in Phase 1. **Arai-Kor-Dai** is the *other* team's name; we inherited their post-office shipping system in Phase 2.

---

## The story

**Phase 1 — built from scratch.** Our 6-person team (team name **Emerald**) designed and built [**SpaceHub**](phase-1-spacehub/), a co-working space management web app, intended to be handed off to *another* team in their Phase 2.

**Phase 2 — inherited someone else's code.** We took over a post-office shipping system built by a *different* team (team **Arai-Kor-Dai**) in their Phase 1. We got it running, moved its database to the cloud, built [**Emerald**](phase-2-emerald-handoff/android-emerald/), a new native Android client, and traced every change request through the system in the [**D4 Impact Analysis**](phase-2-emerald-handoff/d4-impact-analysis/).

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

The **D4 Impact Analysis** is the formal way to show how far a change spreads. It covers the nine change requests of Phase 2:

1. **Traceability graphs** — every requirement linked to the design node, code modules, and tests that realise it, for the whole system and for the affected part.
2. **SLO directed graph** — the 39 affected code files grouped into 10 Software Lifecycle Objects (SLOs: logical modules that are developed, tested, and deployed as a unit), with their dependencies.
3. **Reachability matrix** — the shortest-path distance between every pair of SLOs, which shows which modules a change can reach.
4. **Difficulty analysis** — each change request rated easy or difficult from the modules it touches and how many others reach them.

The result matched what we felt while doing the work: changes to leaf modules were cheap, and changes to the backend core and the database were expensive because almost everything else reaches them.

The **Emerald Android client** was built fresh on top of the inherited backend. The API endpoints stayed the same for the web app and the Android app while the database underneath moved from MySQL to PostgreSQL on Render.

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
| Backend | (Inherited) Express API, moved from MySQL to PostgreSQL on Render in Phase 2 — not in this repo |
| Team size | 6 |

→ See [`phase-2-emerald-handoff/README.md`](phase-2-emerald-handoff/README.md) for the full breakdown and setup instructions.

---

## D4 Impact Analysis (the BA deliverable)

The **D4 Impact Analysis** is the fourth required report of Phase 2. It traces the nine change requests through the inherited system with traceability graphs, an SLO directed graph, and a reachability matrix, then explains which changes were easy or difficult and why.

→ Read it in [`phase-2-emerald-handoff/d4-impact-analysis/D4_IMPACT_ANALYSIS.md`](phase-2-emerald-handoff/d4-impact-analysis/D4_IMPACT_ANALYSIS.md). The four graphs are in the `Impact Analysis imgs/` folder beside it, and their draw.io source is [`phase-2-emerald-handoff/diagrams/TraceabilityGraph-Final.drawio`](phase-2-emerald-handoff/diagrams/TraceabilityGraph-Final.drawio).

---

## Revised November 2026

The course documents were checked against the code and corrected:

- **Phase 1 design document** — the bank-transfer and CCTV integrations are marked as simulated, the encryption mode is AES-256-GCM, the web app and API are described as one Express process, and the component diagram has an errata list.
- **Phase 2 container diagram and traceability graph** — brought in line with the delivered system.
- **D4 Impact Analysis** — the earlier draft was replaced by the final version with its four graphs.

---

## Author

**Rattee Watperatam**
ICT, Faculty of ICT, Mahidol University
Course: **ITCS383** — Year 3 (Jan – May 2026)

[rattee.watp@gmail.com](mailto:rattee.watp@gmail.com) · [github.com/FantasticRattee](https://github.com/FantasticRattee)

## Related work

- [retail-datawarehouse-bi](https://github.com/FantasticRattee/retail-datawarehouse-bi) — Galaxy-schema data warehouse + Tableau BI for a hypothetical 50-branch 7-Eleven Thailand chain
