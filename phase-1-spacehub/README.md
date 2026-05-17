# Phase 1 — SpaceHub (Built from scratch)

A co-working space management web app I co-developed with a 6-person team in **Phase 1** of ITCS383 (Software Construction). The intent was that a *different* team would inherit and extend this codebase in their own Phase 2.

> Team codename: **Emerald** · Period: Aug – Dec 2025 · My role: co-developer

---

## What SpaceHub does

| Role | What they can do |
|---|---|
| **Customer** | Browse desks, book in 3 steps, manage profile, see booking history |
| **Employee** | Check customers in/out, manage equipment inventory |
| **Manager** | Revenue analytics, expense tracking, manage roles/permissions |

All three roles share a single login flow with role-based redirects post-auth.

---

## Tech stack

| Layer | Tech |
|---|---|
| Frontend | Vanilla HTML / CSS / JavaScript (no framework) |
| Backend | Node.js + Express |
| Database | PostgreSQL on Neon (serverless) |
| Auth | bcryptjs (passwords) + AES-256-GCM (PII at rest) |
| Testing | Jest (`server.test.js`) |
| Containerization | Docker |
| CI/CD | GitHub Actions + SonarCloud quality gate |
| Hosting | Render (production) |

---

## Folder layout

```
phase-1-spacehub/
├── README.md                  ← you are here
├── SpaceHub_Project_Map.md    ← system overview I authored
├── code/                      ← the actual web app
│   ├── implementations/       ← Express server + tests
│   │   ├── server.js          (40 KB main server)
│   │   ├── server.test.js     (40 KB Jest tests)
│   │   ├── lib/               (encryption + helpers)
│   │   ├── public/            (static frontend)
│   │   ├── package.json
│   │   ├── Dockerfile
│   │   └── sonar-project.properties
│   ├── designs/               ← design docs (D1)
│   ├── assets/                ← UI assets
│   ├── README.md              ← original team README
│   ├── Emerald_D3_AILog.md    ← how we used AI tooling during construction
│   └── Emerald_D4_QualityReport.md ← coverage + SonarCloud findings
└── docs/                      ← course-issued + presentation
    ├── CoWorkingSpace_UseCase.pdf
    ├── Context  / Container / Component diagrams (PDF)
    ├── SpaceHub_Presentation.pptx
    └── Requirements.txt
```

---

## Run it locally

```bash
cd code/implementations
npm install               # node_modules/ is gitignored
cp .env.example .env      # then fill in your Neon Postgres URL
npm start                 # Express on http://localhost:3000
```

Run the test suite:

```bash
npm test                  # Jest + coverage
```

Build the Docker image:

```bash
docker build -t spacehub .
```

---

## Quality

- **Code quality**: SonarCloud quality gate green (see `code/sonar-project.properties`)
- **Test coverage**: see [`code/Emerald_D4_QualityReport.md`](code/Emerald_D4_QualityReport.md)
- **AI workflow log**: [`code/Emerald_D3_AILog.md`](code/Emerald_D3_AILog.md) — required deliverable documenting how we used AI tooling during construction
