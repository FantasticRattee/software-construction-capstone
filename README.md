# Software Construction — Phase 1 (Build) + Phase 2 (Handoff)

The full greenfield → maintenance cycle, built across two semester phases of **ITCS383 (Software Construction)** at the Faculty of ICT, Mahidol University.

---

## The story

**Phase 1 — built from scratch.** Our 6-person team (codename **Emerald**) designed and built [**SpaceHub**](phase-1-spacehub/), a co-working space management web app, intended to be handed off to *another* team in their Phase 2.

**Phase 2 — inherited someone else's code.** We took over **Arai-Kor-Dai**, a post-office shipping platform built by a *different* team in their Phase 1, and continued development. Before touching the code we produced a formal [**D4 Impact Analysis**](phase-2-emerald-handoff/d4-impact-analysis/), then built [**Emerald**](phase-2-emerald-handoff/android-emerald/) — the new native Android client.

This is the real-world software lifecycle: write clean code knowing someone else will inherit it, then inherit someone else's code and figure it out before changing it.

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
