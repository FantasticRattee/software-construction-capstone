# Phase 2 — Emerald Android + D4 Impact Analysis (Handoff project)

In **Phase 2** of ITCS383, our team (codename **Emerald**) inherited **Arai-Kor-Dai**, a post-office shipping platform built by a *different* team in their own Phase 1. We had to read, analyze, and extend an unfamiliar codebase — the real-world software-maintenance cycle.

> Period: Jan – May 2026 · My role: co-developer of the new Android client

---

## What's here (my contributions)

| Folder | Contents |
|---|---|
| [`android-emerald/`](android-emerald/) | The native Android shipping app I co-developed in Kotlin + Jetpack Compose |
| [`d4-impact-analysis/`](d4-impact-analysis/) | The Business Analysis deliverable I produced *before* touching the inherited code |
| [`diagrams/`](diagrams/) | Component, Container, FileMap (before/after), and final Traceability Graph (draw.io) |
| [`docs/`](docs/) | Course-issued Phase 2 descriptions + Feature Evidences document |

The **inherited Arai-Kor-Dai backend codebase** (built by the other team) is intentionally **not included** in this repo — only my own contributions are shown.

---

## Emerald Android client

A native Android client for the Arai-Kor-Dai post-office shipping platform. Built fresh in Phase 2 to mirror the inherited web app's features on mobile.

| Layer | Tech |
|---|---|
| Language | Kotlin |
| UI | Jetpack Compose + Material3 |
| Networking | Retrofit2 + Coroutines |
| Auth | SessionManager (local token store) |
| Build | Gradle (Kotlin DSL) |
| Target SDK | 26–36 |
| Testing | JUnit 5 + MockK + JaCoCo coverage |
| CI | GitHub Actions + SonarCloud |
| Backend | (Inherited) Express + MySQL — not in this repo |

### Features

- User registration + login (bound to the inherited backend)
- Shipping orders — parcel booking, identity verification (national ID + selfie), price calc
- Real-time payment — PromptPay, credit card, e-wallet (via inherited API)
- Parcel tracking + shipment history
- PDF shipping-label rendering with QR codes

### Run it locally

```bash
cd android-emerald
./gradlew assembleDebug    # produces a debug APK in app/build/outputs/
```

Or open `android-emerald/` in **Android Studio** for the full development experience.

> `app/build/` and `.gradle/` are gitignored — first build will populate them.

---

## D4 Impact Analysis (the BA deliverable)

Before any code changes to the inherited Arai-Kor-Dai codebase, we produced the **D4 Impact Analysis** — a formal Business Analysis document identifying:

- **Dependencies** — what each module relies on (file map, before vs after)
- **Risks** — failure modes and blast radius if we broke the contracts
- **SLOs** — Service Level Objectives we needed to honor on the inherited service
- **Reachability matrix** — what code is reachable from each user-facing feature
- **Proposed changes** — minimal, traceable extensions

Find it here:

- [`d4-impact-analysis/D4_IMPACT_ANALYSIS.md`](d4-impact-analysis/D4_IMPACT_ANALYSIS.md) — the analysis itself
- [`d4-impact-analysis/D4_IMPACT_ANALYSIS_GRAPHSupdate_connected_v2.drawio`](d4-impact-analysis/) — the connected reachability graph

The traceability graphs went through 7 iterations during D4 work; only the final **"Done"** version is kept in [`diagrams/TraceabilityGraph-Final.drawio`](diagrams/TraceabilityGraph-Final.drawio).

---

## Diagrams

| File | What it shows |
|---|---|
| `Emerald_Phase2_Component_Diagram.drawio` | Components inside the Android client |
| `Emerald_Phase2_Container_Diagram.drawio` | Android client ↔ inherited backend ↔ database |
| `Emerald_Phase2_FileMap_BeforeAfter.drawio` | Inherited file structure → our additions |
| `TraceabilityGraph-Final.drawio` | Final reachability matrix for D4 |

Open them with [draw.io](https://app.diagrams.net/) or the desktop app.

---

## Course documents

- [`docs/Project Phase 2 Description Part 1.pdf`](docs/) — course-issued Phase 2 specification (Part 1)
- [`docs/Project Phase 2 Part 2 (The Maintenance) Description.pdf`](docs/) — course-issued Phase 2 specification (Part 2 — Maintenance)
- [`docs/Project Phase 2 Part 2 (The Maintenance) Slides.pdf`](docs/) — course-issued slide deck for Part 2
- [`docs/Feature-Evidences.docx`](docs/Feature-Evidences.docx) — Phase 2 Part 1 Feature Evidences document
