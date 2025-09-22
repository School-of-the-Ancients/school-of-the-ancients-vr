# School of the Ancients — Citation‑First VR Tutor

> **Embodied, source‑grounded lessons.** A self‑managed VR academy where AI teachers run Socratic lessons, adapt to each learner, and **always show citations**. A Matrix‑style **Operator** can spawn rooms, props, quizzes, and live edits during class.

---

## Quick links
- [Vision & Purpose](#vision--purpose)
- [Core Capabilities](#core-capabilities)
- [Architecture at a Glance](#architecture-at-a-glance)
- [Performance & Reliability Targets](#performance--reliability-targets)
- [Operator Commands](#operator-commands)
- [Roles & Access](#roles--access)
- [Getting Started (WIP)](#getting-started-wip)
- [Repository Layout (suggested)](#repository-layout-suggested)
- [Roadmap](#roadmap)
- [Acknowledgements & Sources](#acknowledgements--sources)

---

## Vision & Purpose

Traditional online courses struggle to keep attention, personalize difficulty, and cite sources transparently. **School of the Ancients** addresses this by turning lessons into **embodied, in‑character conversations** with **citation‑first** answers. Target users include **students (13+)**, **lifelong learners**, **educators/creators**, and **institutions** (museums/schools). Why this instead of alternatives? **Embodiment + agency**, **Socratic adaptivity** with visible **citations**, **operator‑speed** edits during class, and **remixable/extensible** content packs.

## Core Capabilities

- **AI‑Powered Historical/Scientific Figures** — LLM‑based personas with ethical boundaries and source grounding.
- **Socratic Learning Loops** — Adaptive questioning, oral assessment, mastery tracking.
- **Citation‑First Content** — RAG over vetted texts; transparent source attribution.
- **Matrix Operator System** — Real‑time world modification: spawn assets, launch quizzes, lay out scenes, freeze for safety, save snapshots.

## Architecture at a Glance

A **distributed, event‑driven microservices** approach separates VR rendering, AI processing, content management, and real‑time sync. Core components:

- **VR Frontend** — Unity/OpenXR (port) or Horizon Worlds (now). Maintains immersive 72/90Hz frame budget.
- **OperatorServer** — FastAPI or Node service exposing HTTP + WebSocket; orchestrates sessions and commands.
- **AI Tutoring Engine** — In‑character dialogue, adaptive difficulty, assessment handoff.
- **RAG Citation System** — Supabase/Postgres (pgvector) + embeddings; 100% citation traceability.
- **Content & Assets** — Object storage/CDN for lesson packs, realms, and media.
- **Analytics & Observability** — Prometheus/Loki/Tempo + OpenTelemetry; per‑role dashboards.

**Key data flows** (high level):

1. **Student interaction** → VR sends message over **WebSocket** to OperatorServer → AI Tutoring Engine generates response.
2. **Content retrieval** → AI triggers **vector similarity** search → returns grounded context **with citations**.
3. **Real‑time sync** → OperatorServer broadcasts state to all clients for multi‑user sessions.
4. **Assessment** → Mastery and progress → analytics + storage.

## Performance & Reliability Targets

- **Operator command echo**: **< 150 ms**  
- **AI first token**: **< 1.5 s** end‑to‑end  
- **VR frame rate**: **72/90 Hz** sustained  
- **Uptime (Operator/LLM endpoints)**: **≥ 99.5%**  
- **Multi‑user sessions**: **Up to ~70 concurrent students/room** (scales via session sharding/recorded presence)

## Operator Commands

Common live‑edit controls (voice/UI):

```
spawn_asset <id>
layout <verb> [args]
attach_behavior <asset> <behavior>
quiz.start <assessment_id>
safety.freeze
save_scene
```

## Roles & Access

- **Student** — Learner HUD with *Why?*, *Hint*, *Show source*, progress ring, pause.
- **Teacher/Creator** — Persona sliders (tone/depth), scope controls, safety toggles, *Test lesson*.
- **Operator (Admin)** — Command console, logs, undo, freeze, save.
- **Autonomous AI (restricted)** — Runs only sandboxed commands under policy.

**Authentication**: Platform SSO (Meta) for Horizon; OAuth/SAML/OIDC for Unity builds and institutional pilots.  
**Authorization**: Role‑based access; sudo requires explicit grant + audit logs.  
**Business rules**: **Citations‑first**; prefer public‑domain/cleared sources; no impersonation of living persons without rights/consent; age gates and safety filters.

## Getting Started (WIP)

> This is a **skeleton** to be adapted to your codebase. The spec supports either **FastAPI** or **Node** for the OperatorServer and **Unity/OpenXR** or **Horizon Worlds** for the VR front end.

### Prerequisites

- **Backend**: Python 3.11 + FastAPI *or* Node 18+  
- **Database**: Postgres 14+ with **pgvector** (Supabase recommended)  
- **Cache**: Redis (session + vector result caching)  
- **VR**: Unity 2022+ (OpenXR, XR Interaction Toolkit) *or* access to Horizon Worlds  
- **AI**: Provider keys (e.g., OpenAI/Anthropic); STT/TTS provider keys

### Example `.env` (OperatorServer)

```bash
# Core
APP_ENV=dev
PORT=8000

# Auth
JWT_SECRET=change-me
OAUTH_CLIENT_ID=...
OAUTH_CLIENT_SECRET=...

# Data & RAG
DATABASE_URL=postgresql://user:pass@localhost:5432/sota
PGVECTOR_ENABLED=true
REDIS_URL=redis://localhost:6379
ASSET_CDN_BASE=https://cdn.example.com

# AI
OPENAI_API_KEY=...
ANTHROPIC_API_KEY=...
```

### Run (FastAPI example)

```bash
pip install -r operator-server/requirements.txt
uvicorn operator_server.main:app --reload --port 8000
# WebSocket: /ws/education/{session_id}
```

### Unity (OpenXR) notes

- Import XR Interaction Toolkit, set OpenXR, and target Quest/PCVR.  
- Connect to OperatorServer WebSocket and implement the Operator command contract.

## Repository Layout (suggested)

```
.
├─ operator-server/          # FastAPI/Node implementation of OperatorServer
├─ vr-frontend/              # Unity project (OpenXR); Horizon worlds assets live separately
├─ rag/                      # Indexers, embedding jobs, source ingestion
├─ lesson-packs/             # Realm templates, figures, assessments, provenance
├─ docs/                     # Specs, diagrams, decision records
└─ tools/                    # Dev scripts (DB migrations, test fixtures)
```

## Roadmap

**High**: Socratic Q&A + citations; Operator core (spawn_asset/layout/quiz.start/save); 3 starter realms (Cleopatra, Galileo, Leonardo); mastery checks; creator publishing; safety layer.  
**Medium**: Voice I/O; cohort mode; dashboard + spaced repetition; provenance badges.  
**Lower**: Marketplace; achievements; advanced animation; multi‑scene quests.

## Acknowledgements & Sources

This README condenses and organizes material from the project’s **build prompt** and **target technical specification**. See the repo’s `/docs` folder for the full originals.
