# School of the Ancients (SotA)

**Immersive, citation-first VR learning**: AI instructors emulate historical & influential figures and teach inside dynamically orchestrated virtual worlds. A “Matrix Operator” lets educators reshape scenes in real time with voice or text, while a RAG pipeline guarantees every claim is backed by verifiable sources.

> *Built for Quest 3/Pro and PCVR; integrates with LMS via LTI 1.3; ships with multiplayer seminars, creator tools, and enterprise-grade observability.*

---

## Table of Contents
- [Why SotA?](#why-sota)
- [Core Features](#core-features)
- [System Architecture](#system-architecture)
- [Tech Stack](#tech-stack)
- [Getting Started (Dev)](#getting-started-dev)
- [Repository Layout](#repository-layout)
- [Development](#development)
- [Testing](#testing)
- [Deployment](#deployment)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Why SotA?
Traditional e-learning lacks context, mentorship at scale, and trustworthy sourcing. SotA merges **VR + Generative AI** to deliver adaptive instruction with **verifiable citations** and **real-time world orchestration**. Institutions get measurable outcomes, compliance, and private deployments; creators get “sudo” worldbuilding with safety rails.

---

## Core Features
- **VR Classroom (Unity XR)** — 72–90 FPS target, body transformers/locomotion mediator, Addressables + CDN streaming.  
- **Matrix Operator** — Voice/text commands to *spawn assets, modify scenes, attach behaviors, adjust lighting/physics* in <2 s, with rollback and safety checks.  
- **AI Teachers (Personas)** — Historically authentic emulation with guardrails, disclaimers, and adaptive pedagogy.  
- **Citation-First RAG** — PostgreSQL + pgvector; sub-500 ms vector queries; provenance, licensing, & audit trails baked in.  
- **Multiplayer Seminars** — Photon Fusion (shared authority / client-host / dedicated server) with integrated voice.  
- **Creator Console (Web)** — No-code lesson/world builder, auto license validation, moderation pipeline, marketplace-ready publishing.  
- **Assessments & Analytics** — Knowledge graphs, mastery tracking, dashboards; OpenTelemetry across app/infra.  
- **Enterprise Integrations** — LTI 1.3 (OAuth/OIDC, grade passback), SSO (Auth0/SAML), S3-compatible storage, RBAC, compliance (FERPA/COPPA/GDPR).

> KPIs: >25% retention lift vs baseline, >80% session completion, <120 ms operator round-trip, 100% citation coverage.

---

## System Architecture
- **Clients**: Unity XR Frontend (Quest/PCVR) + React Creator Console.  
- **Core Services**: Matrix Operator (FastAPI), AI Orchestrator (multi-agent), RAG Pipeline (Postgres + pgvector), Session/Multiplayer (Photon).  
- **Data**: Postgres 15 + pgvector 0.8 (HNSW/IVFFlat, iterative index scans), Redis caching, S3 for assets via CDN.  
- **Infra**: AWS ECS Fargate, ALB/NLB, CloudFront, RDS, Secrets Manager, IaC via Terraform, OpenTelemetry → Prometheus/Jaeger/Grafana.  
- **Security**: TLS 1.3, JWT/OIDC, RBAC, DRM/watermarking, circuit breakers & graceful degradation.

*(See the high-level dataflow and session state diagrams — e.g., architecture/data-flow around pp. 90–93, 115–118.)*

---

## Tech Stack
- **VR/XR**: Unity 2022.3 LTS, XR Interaction Toolkit 3.x, Addressables  
- **Networking**: Photon Fusion + Photon Voice  
- **Backend**: Python 3.11, FastAPI, LangChain  
- **Data**: PostgreSQL 15, pgvector 0.8, Redis  
- **Web**: React 18, TypeScript 5, TailwindCSS, Vite  
- **Auth/LMS**: LTI 1.3, OAuth2/OIDC, Auth0/SAML  
- **Observability**: OpenTelemetry, Prometheus, Jaeger, Grafana  
- **Cloud**: AWS (ECS Fargate, RDS, S3/CloudFront, Secrets Manager), Terraform

---

## Getting Started (Dev)

> **Prereqs**: Unity 2022.3 LTS, Node 18+, Python 3.11, Docker, Postgres 15, Redis.

```bash
# 1) Backend (FastAPI + RAG)
cp .env.example .env  # fill OpenAI keys, DB URLs, Auth configs
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

**Quick test**  
- Hit `http://localhost:8000/health` (OK)  
- Visit `http://localhost:5173` (Creator Console)  
- In Unity, run a sample scene and say: *“Operator, load Renaissance Florence.”*

---

## Repository Layout
```
/unity/                 # Unity XR client (scenes, prefabs, Addressables)
/app/                   # FastAPI services (Matrix Operator, Orchestrator, RAG)
/web/                   # React Creator Console + Admin
/db/                    # Migrations, schema, seeds, vector indexes
/scripts/               # Ingestion, evaluation, tooling
/infra/terraform/       # AWS modules (VPC, ECS, RDS, CloudFront, etc.)
/observability/         # OTEL collector, dashboards, alerts
```

---

## Development
- **Matrix Operator tools**: `spawn_skybox`, `spawn_asset`, `attach_behavior`, `set_physics`, `modify_ui` (guarded by permissions & safety).  
- **Content workflow**: Source import → license validation → chunk/embeddings → publish; moderation + audit trail.  
- **Performance targets**: Operator <120 ms round-trip; RAG <500 ms; VR 72–90 FPS (LOD, occlusion, async streaming).

---

## Testing
- **Unity**: Play/Edit mode tests + performance harness (frame-rate, motion-to-photon).  
- **Backend**: pytest (unit/integration); Testcontainers (pgvector), OpenAI API fixtures.  
- **E2E**: LTI launch → VR session init → Operator commands → assessment/grade passback.  
- **Quality gates**: 100% citation for instructional claims; zero safety violations; accessibility (WCAG 2.1 AA).

---

## Deployment
- **AWS ECS Fargate** (blue/green or canary), RDS Multi-AZ, CloudFront CDN for Addressables.  
- **Secrets**: AWS Secrets Manager; **IaC**: Terraform modules; **Auto-scaling** on CPU/memory/latency/FPS.  
- **Compliance**: FERPA/COPPA/GDPR (data retention, masking, consent, export/erasure).  
- **Observability**: OTEL → Prometheus/Jaeger/Grafana; alerts via PagerDuty/Slack.

---

## Roadmap
- **Phase 2**: Mobile/AR companion, advanced NPC behaviors, new subjects.  
- **Phase 3**: OpenUSD + verifiable credentials, marketplace connectors.  
- **Phase 4**: Modding SDK, community content, deeper AI reasoning.

---

## Contributing
Issues and PRs are welcome. Please run tests locally, include schema/migration updates where needed, and follow the style & safety checklists (citations, moderation flags, accessibility).

---

## License
TBD — include your chosen OSS or commercial license here. Ensure third-party assets respect their original terms.

---

## Acknowledgments
Unity XR Team; Photon; OpenAI; 1EdTech LTI community; OpenTelemetry; Wikimedia/Internet Archive/Project Gutenberg (for public-domain/CC sources); and early educators/learners who piloted the approach.
