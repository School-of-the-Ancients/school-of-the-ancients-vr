# School of the Ancients (SotA)

**Immersive, citation-first VR learning.** AI teachers emulate historical & influential figures and teach inside dynamically orchestrated worlds. A Matrix-style **Operator** lets you change scenes with voice/text. Every instructional claim shows **verifiable citations**.

> Target: Quest 3/Pro + PCVR • LTI 1.3 for LMS • Multiplayer seminars • Creator tools • Observability (OpenTelemetry)

---

## Why
Online courses are passive and one‑size‑fits‑all. SotA combines **VR + Generative AI** to deliver adaptive instruction with **sources you can trust**, world orchestration, and measurable outcomes for schools and creators.

---

## Core Features
- **VR Classroom (Unity XR 3.x)** — 72–90 FPS target, Near‑/Far interaction, locomotion mediator, Addressables + CDN.
- **Matrix Operator** — Voice/text commands to *spawn assets, modify scenes, attach behaviors, tweak lighting/physics* (<2 s apply, <120 ms tool latency target).
- **AI Teachers (Personas)** — Historically authentic emulation with guardrails, disclaimers, and adaptive pedagogy.
- **Citation‑First RAG** — Postgres + **pgvector 0.8**; sub‑500 ms vector queries; provenance, licensing, & audit trails.
- **Multiplayer Seminars** — Photon Fusion + Voice (shared/host/dedicated topologies).
- **Creator Console (Web)** — No‑code lesson/world builder, license validation, moderation pipeline, publish.
- **Assessments & Analytics** — Knowledge graphs, mastery tracking, dashboards; OpenTelemetry across app/infra.
- **Enterprise** — LTI 1.3, OAuth/OIDC/SAML SSO, RBAC, S3-compatible storage, compliance (FERPA/COPPA/GDPR).

**KPIs**: >25% retention lift, >80% session completion, <120 ms operator round‑trip, **100% citation coverage**.

---

## System Architecture (High level)
- **Clients**: Unity XR Frontend (Quest/PCVR) + React Creator Console.
- **Core Services**: Matrix Operator (FastAPI), AI Orchestrator (multi‑agent), RAG Pipeline (Postgres+pgvector), Session/Multiplayer (Photon).
- **Data**: PostgreSQL 15 + pgvector 0.8 (HNSW + iterative scans), Redis cache, S3 asset store/CDN.
- **Infra**: AWS ECS Fargate, RDS, CloudFront, Secrets Manager, Terraform, OpenTelemetry → Prometheus/Jaeger/Grafana.
- **Security**: TLS 1.3, JWT/OIDC, RBAC, DRM/watermarking, circuit breakers & graceful degradation.

See diagrams (data flow, state, and integration) in the Technical Spec for details (Operator flow, RAG pipeline, LTI auth).

---

## Tech Stack
**VR/XR**: Unity 2022.3 LTS, XR Interaction Toolkit 3.x, Addressables  
**Networking**: Photon Fusion + Photon Voice  
**Backend**: Python 3.11, FastAPI, LangChain  
**Data**: PostgreSQL 15, pgvector 0.8, Redis  
**Web**: React 18, TypeScript 5, TailwindCSS, Vite  
**Auth/LMS**: LTI 1.3, OAuth2/OIDC, Auth0/SAML  
**Observability**: OpenTelemetry, Prometheus, Jaeger, Grafana  
**Cloud**: AWS ECS Fargate, RDS, S3/CloudFront, Secrets Manager, Terraform

---

## Getting Started (Dev)

> **Prereqs**: Unity 2022.3 LTS, Node 18+, Python 3.11, Docker, Postgres 15, Redis.

```bash
# 1) Backend (FastAPI + RAG)
cp .env.example .env     # Fill OpenAI keys, DB URLs, auth configs
docker compose up -d db redis
uvicorn app.main:app --reload

# 2) Vector DB (pgvector)
# ensure extension enabled; create schema & indexes
psql $DATABASE_URL -f db/schema.sql
python scripts/ingest_sources.py data/ --embeddings openai

# 3) Web (Creator Console)
cd web && pnpm i && pnpm dev

# 4) Unity (VR Client)
# Open project in Unity, set XR Plugin Management, play-in-editor or deploy to Quest/PCVR
```

**Smoke tests**
- `GET /health` → OK  
- Creator Console at `http://localhost:5173`  
- In Unity: *“Operator, load Renaissance Florence.”*

---

## Repository Layout
```
/unity/                 # Unity XR client (scenes, prefabs, Addressables)
/app/                   # FastAPI services (Matrix Operator, Orchestrator, RAG)
/web/                   # React Creator Console + Admin
/db/                    # Migrations, schema, vector indexes
/scripts/               # Ingestion, evaluation, tooling
/infra/terraform/       # AWS modules (VPC, ECS, RDS, CloudFront, etc.)
/observability/         # OTEL collector, dashboards, alerts
```

---

## Development Notes
- **Operator tools**: `spawn_skybox`, `spawn_asset`, `attach_behavior`, `set_physics`, `modify_ui` (RBAC + safety).  
- **Content pipeline**: Import → license validate → chunk/embed → publish; moderation + audit trail.  
- **Perf targets**: Operator <120 ms; RAG <500 ms; VR 72–90 FPS (LOD, occlusion, async streaming).  
- **LTI 1.3**: OIDC launch, JWT validation, Deep Linking, Names/Roles, Assignments/Grades.

---

## Testing
- **Unity**: Play/Edit mode + performance harness (frame‑rate, motion‑to‑photon).  
- **Backend**: pytest (unit/integration); Testcontainers (pgvector); OpenAI fixtures.  
- **E2E**: LTI launch → VR session → Operator commands → assessment → grade passback.  
- **Quality gates**: **100% citation** for instructional claims; zero safety violations; WCAG 2.1 AA.

---

## Deployment
- **AWS ECS Fargate** (blue/green or canary), RDS Multi‑AZ, CloudFront for Addressables.  
- **Secrets**: AWS Secrets Manager • **IaC**: Terraform • **Auto‑scaling**: CPU/mem/latency/FPS.  
- **Compliance**: FERPA/COPPA/GDPR; data retention & export/erasure.  
- **Obs**: OTEL → Prometheus/Jaeger/Grafana; alerts (PagerDuty/Slack).

---

## Roadmap
- **Near-term**: Mobile/AR companion, advanced NPC behaviors, new subjects.  
- **Next**: OpenUSD + verifiable credentials, marketplace connectors.  
- **Later**: Modding SDK, community content, deeper reasoning.

---

## Contributing
Issues & PRs welcome. Please run tests, include schema/migrations as needed, and follow style & safety checklists (citations, moderation flags, accessibility).

---

## License
TBD — add your OSS or commercial license. Ensure third‑party assets respect their terms.

---

## Acknowledgments
Unity XR • Photon • OpenAI • 1EdTech LTI • OpenTelemetry • Wikimedia, Internet Archive, Project Gutenberg (for PD/CC sources) • Early educators & learners.

_Source: product brief and technical specs._
