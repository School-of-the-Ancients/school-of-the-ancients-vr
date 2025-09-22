# School of the Ancients (SoTA)

Immersive, citation‑first VR learning where AI teachers (historical & scientific figures) guide Socratic lessons in living, explorable worlds.

---

## ✨ What is it?
**School of the Ancients** is a self‑managed VR academy. Learners enter historical or scientific realms, converse with an in‑character AI teacher, get **Socratic Q&A**, and see **sources up front**. Creators/teachers can spin up lessons live with an **Operator console** that spawns assets, edits layouts, deploys quizzes, and saves scenes during class.

> Why this matters: On‑line courses struggle with attention, personalization, and transparent sourcing. SoTA solves that with embodiment, adaptivity, and **citation‑first** answers.

---

## 🧭 Tracks & Core Components
- **Track A (now):** _Meta Horizon Worlds_ world + panels/UI (TypeScript in Desktop Editor)  
- **Track B (port):** _Unity (OpenXR, XR Interaction Toolkit)_ with Photon/Normcore multiplayer

**Backend & AI**
- **OperatorServer:** FastAPI + WebSockets (sub‑150 ms command echo)
- **AI Tutoring Engine:** Socratic loops, adaptive difficulty, persona boundaries
- **RAG Citation System:** Supabase/PostgreSQL + pgvector for vetted sources
- **Storage/CDN:** Object storage for lesson assets; logs/telemetry for QA

**Roles**
- _Student_, _Creator/Teacher_, _Operator (Admin)_, _Autonomous AI (restricted)_

---

## 🏗️ Architecture at a glance
- **VR Frontend** ↔ **OperatorServer (WS)** ↔ **AI Engine** ↔ **RAG/Vector DB**
- **Key flows**
  1. **Learn a lesson:** pick figure → enter realm → Socratic loop → checks → mastery % + sources
  2. **Create a realm:** template → add figure → upload sources → generate lesson pack → publish
  3. **Live edit:** `spawn_asset`, `layout`, `quiz.start`, `safety.freeze`, `save_scene`

**Performance targets**
- **VR frame rate:** 72/90 Hz  
- **AI first token:** < 1.5 s  
- **Operator echo:** < 150 ms  
- **Uptime:** 99.5% for core endpoints

---

## 🧩 Tech Stack
**Frontend (VR)**
- Unity 2022.3 LTS+ (OpenXR), XR Interaction Toolkit 2.5+, Photon/Normcore (multi‑user)
- Meta XR SDKs (Track A), TypeScript panels (Horizon Worlds)

**Backend & Data**
- Python 3.11+, FastAPI 0.104+ (WS), Uvicorn
- PostgreSQL 15+ with **pgvector** (HNSW indexes) via Supabase
- Redis 7 (sessions/pubsub), Cloud CDN for assets
- LangChain orchestration; OpenAI/Anthropic LLMs; STT/TTS provider(s)

---

## 🚀 Quickstart (dev)

> These steps assume Docker is installed; swap in your own keys and providers.

```bash
# 1) Clone and scaffold environments
git clone <your-fork> sota && cd sota
cp .env.example .env            # fill: DB url, OpenAI key, etc.

# 2) Start core services
docker compose up -d postgres redis

# 3) Launch OperatorServer
docker compose up -d operator

# 4) Run RAG bootstrap (ingest vetted PDFs/text)
python tools/ingest.py data/sources/

# 5) Start Unity (Track B) or open Horizon Worlds (Track A)
#   - Unity: open /unity/ project, set OpenXR, press Play
#   - Horizon: open world in Desktop Editor, connect to OperatorServer URL
```

**Common ports**
- OperatorServer: `:8000` (HTTP) / `WS /ws/{session_id}`
- Postgres: `:5432` (pgvector enabled)  
- Redis: `:6379`

---

## 🕹️ Operator Commands (runtime)
- `spawn_asset {type, position}` — place a 3D prop / artifact
- `layout {config}` — change seating/scene layout
- `attach_behavior {id, behavior}` — simple scripted behaviors
- `quiz.start {assessment_id}` / `quiz.end` — deploy or finish a check
- `safety.freeze` — emergency halt (mute interactions)
- `save_scene` — snapshot current realm state

> These are issued via WS to OperatorServer; VR clients receive deltas and render immediately.

---

## 📚 RAG & Citations
- Import public‑domain or licensed sources → chunk + embed → **vector search** at answer time  
- All **factual claims** surface source title/link + verification flag in the VR HUD and logs
- Content QA jobs validate citation coverage and age‑appropriateness before publish

---

## ✅ Acceptance & SLAs
- **Educational efficacy:** measurable gains (pre/post), mastery progression dashboard
- **Content integrity:** 100% citation traceability; PD/licensed priority
- **Privacy:** COPPA/FERPA aware roles, audit logs, PII minimization
- **Reliability:** autosave every 2 min; DR objectives for student progress

---

## 📦 Suggested repo layout
```
/operator/         # FastAPI app (WS routes, auth, RBAC)
/ai/               # Socratic engine, persona configs, adapters
/rag/              # Ingest, chunking, embeddings, evaluators
/unity/            # OpenXR project (Track B)
/horizon/          # TS panels & scripts (Track A)
/tools/            # CLI: ingest, eval, fixtures
/deploy/           # docker-compose, k8s manifests, CI
/docs/             # product docs, personas, UX flows
```

---

## 🔐 Compliance & Safety
- Role‑based access with audit trails; age gates for under‑13
- Moderation: profanity/harassment filters; bias checks with human review queue
- Data retention & export (parental requests), disaster recovery, and health checks

---

## 🧪 Testing & Perf
- Unit/integration for WS flows, RAG retrieval, and Socratic loops
- Perf gates: 90 Hz target (PCVR) / 72 Hz (Quest), WS echo < 150 ms, p95 AI < 1.5 s
- Observability: Prometheus/Grafana; tracing across VR → Operator → AI → DB

---

## 🗺️ Roadmap (abridged)
- **High:** Socratic Q&A + citations; Operator core; 3 starter realms (Cleopatra, Galileo, Leonardo); mastery checks; publishing; safety layer
- **Medium:** Voice I/O end‑to‑end; cohort mode; dashboards & spaced repetition; provenance badges
- **Lower:** Marketplace, badges gallery, multi‑scene quests

---

## 🤝 Contributing
PRs welcome! Please:
1) Keep lessons **citation‑first**.  
2) Avoid live impersonation of living people without rights/consent.  
3) Meet perf budgets (frame rate, AI latency).  
4) Include tests and docs.

---

## 📝 License
Choose a permissive license for code and a provenance‑aware license for content packs (PD/CC‑BY preferred).

---

## Acknowledgements
Built from the **School of the Ancients v3** spec and planning docs. See /docs for the full technical specification, UX flows, and compliance notes.
