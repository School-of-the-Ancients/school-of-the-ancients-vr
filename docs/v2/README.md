# School of the Ancients
_Autonomous AI Company + VR Learning Platform powered by Socratic dialogue and historical AI teachers_

> Learn by sparring with history’s greatest minds inside immersive, accurate virtual worlds.  
> **Matrix Operator** commands like _“Load the Renaissance and spawn Leonardo da Vinci”_ create the scene; AI teachers guide you with adaptive, Socratic Q&A.

---
## ✨ What’s in this repo
- **VR Client (Unity/OpenXR)** — immersive environments, spatial UI, and multi‑user classrooms.
- **AI Teachers Service (FastAPI + OpenAI)** — character emulation (Socrates, Hypatia, Leonardo…), adaptive Socratic dialogue, safety filters.
- **Assessment Engine** — real‑time knowledge checks, mastery tracking, personalized learning paths.
- **Matrix Operator** — natural‑language voice/text commands to load worlds and spawn teachers.
- **Educational Integrations** — SSO + LMS (LTI 1.3, Canvas, Moodle), learning analytics, grade passback.
- **Infra as Code** — Docker/K8s, pgvector/Postgres, Redis, CDN, Observability, CI/CD.

---
## 🧠 Vision (TL;DR)
Education shouldn’t feel like downloading slides. It should feel like a **conversation**—in context, in world, and at your level. _School of the Ancients_ turns history, science, and philosophy into **dialogue-first lessons** inside living, period‑accurate VR scenes. The system adapts difficulty in real time and supports **multi‑student classrooms**.

---

## Product prompt seed
# **School of the Ancients — Product Specification**

**Date:** 9/21/25\
**Concept:** Autonomous AI Company + School of the Ancients VR + Matrix Operator

---

## **WHY – VISION & PURPOSE**

**What problem are you solving and for whom?**\
Education today often feels static, text-heavy, and disconnected from lived experience. Students struggle with engagement, retention, and critical thinking when faced with rote memorization and lecture formats. *School of the Ancients* solves this by making learning interactive, personalized, and immersive. It brings history, science, and philosophy to life through AI-driven roleplay, turning learning into a dialogue rather than a download. This is designed for students, lifelong learners, and educators seeking engaging, adaptive teaching tools.

**What does your application do?**\
*School of the Ancients* is a self-managed VR learning environment run by an autonomous AI company. It emulates historical figures, inventors, scientists, and philosophers as teachers, each creating their own character prompts and teaching their fields in-character. Lessons unfold Socratically — through question-and-answer exchanges — with AI adapting content to the learner’s knowledge. The Matrix Operator system loads custom VR worlds (“Load the Renaissance,” “Enter the Roman Agora”) where these AI figures teach interactively.

**Who will use it?**

- **Students** (middle school to university) seeking engaging and personalized ways to learn history, science, and philosophy.

- **Educators** who want AI co-teachers or dynamic VR classrooms.

- **Lifelong learners** curious about exploring knowledge in an immersive, game-like environment.

- **Developers/creators** who want to extend the system by adding new AI teachers or custom domains.

**Why will they use it instead of alternatives?**\
Unlike e-learning platforms (Coursera, Khan Academy), *School of the Ancients* provides:

- **Immersion**: Students *meet* and *debate with* Socrates, Einstein, or Cleopatra in their historical settings.

- **Personalization**: Curriculum adapts dynamically based on learner knowledge and choices.

- **Agency**: Users or AI have sudo privileges in the Matrix Operator, reshaping worlds and lessons on demand.

- **Critical thinking focus**: Socratic Q&A encourages reasoning, not rote answers.

- **Extensibility**: Any historical or influential figure can be added as a VR teacher, expanding endlessly.

---

## **WHAT – CORE REQUIREMENTS**

**What must your application do?**

- System must emulate historical figures as AI-driven VR teachers.

- System must deliver Socratic-style Q&A interactions.

- Users must be able to request environments via Matrix Operator voice/text commands.

- System must evaluate student knowledge and adapt difficulty.

- Users must be able to progress through a curriculum with branching paths.

- System must support multi-user VR classrooms.

**What actions need to happen?**

- User enters VR/AR environment.

- Operator spawns requested world and historical NPC.

- NPC engages learner in adaptive Socratic dialogue.

- Knowledge assessment updates curriculum path.

- System logs progress and generates reports.

- Optional: multiple users join shared debates or classrooms.

**What should the outcomes be?**

- Learners achieve deeper understanding through guided questioning.

- Knowledge retention improves via immersive, embodied learning.

- Students feel curiosity and motivation comparable to gameplay.

- Educators gain a scalable AI co-teaching assistant.

- The autonomous AI company self-manages curricula, iterates based on results, and improves continuously.

---

## **HOW – PLANNING & IMPLEMENTATION**

**What are the required stack components?**

- **Frontend (VR/AR):** Unity or Unreal Engine; VRIF/XRI for interaction; OpenXR support.

- **Backend:** Node.js / Python APIs; Supabase (data logging, progress tracking); Temporal (workflow orchestration).

- **AI Models:** OpenAI GPT-5 (character emulation + Socratic dialogue); Qdrant/pgvector (memory retrieval for historical accuracy).

- **Matrix Operator:** HTTP/WS runtime server with prefab loaders (Unity Addressables, glTFast).

- **Infrastructure:** Dockerized services (Postgres, Qdrant, Redis); DigitalOcean/AWS hosting.

**What are the system requirements?**

- **Performance:** Low-latency dialogue in VR; target &lt;300ms response time.

- **Scalability:** Multi-user sessions; ability to support classroom groups of 20+.

- **Security:** Role-based access; student data privacy (FERPA/GDPR compliance).

- **Reliability:** 99.9% uptime for backend services; session persistence for lesson continuity.

- **Integration:** Must integrate with existing VR assets, voice AI, and educational LMS platforms (Canvas, Moodle).

**What are the key user flows?**

1. **Student Flow:**

   - Entry: User dons headset, chooses subject.

   - Operator loads world + teacher NPC.

   - NPC begins Socratic Q&A based on knowledge level.

   - Student answers, debates, explores.

   - NPC adapts lesson, tracks progress.

   - Exit: Session summary + suggested next steps.

2. **Educator Flow:**

   - Teacher creates class module.

   - Students enter shared VR classroom.

   - Teacher + AI NPC co-facilitate learning.

   - Reports generated for student progress.

**What are the core interfaces?**

- **Matrix Operator Console:** For spawning worlds, teachers, and lessons.

- **VR Learning Environment:** Main student interface; immersive classrooms, debates, experiments.

- **Curriculum Dashboard:** Educator view for progress tracking, adjusting difficulty, reviewing logs.

- **AI Company Backend:** Self-optimization system managing lesson libraries, metrics, and agentic roles.

---

## **BUSINESS REQUIREMENTS**

**What are your access and authentication needs?**

- User types: Students, Educators, Admins, Developers.

- Authentication: SSO for schools; OAuth2 for general users.

- Access Control: Role-based privileges (sudo rights for creator/AI, limited rights for learners).

**What business rules must be followed?**

- Historical content must be accurate (validated by RAG knowledge base).

- Lesson difficulty must adapt based on assessment results.

- NPCs must remain within educational/ethical boundaries (no unsafe or harmful advice).

- Compliance with education standards (FERPA, GDPR, COPPA).

- SLA: 99.9% uptime, data backed up daily.

**What are your implementation priorities?**

- **High Priority:** Core Socratic dialogue engine, Matrix Operator world loading, AI historical figure emulation, knowledge assessment loop.

- **Medium Priority:** Multiplayer classrooms, educator dashboards, lesson expansion packs (science, philosophy, leadership).

- **Lower Priority:** Alternate-history simulations, gamified achievements, “AI company” self-optimization dashboards.

---

## 🏗️ Architecture (high level)
- **Client:** Unity 6+ (URP) with **OpenXR**; XR Interaction Toolkit; diegetic + spatial UI; target **90+ FPS**.
- **AI Layer:** OpenAI GPT‑5 family (full/mini/nano) with cost‑aware routing, reasoning depth control, and **prompt caching**.
- **RAG/Memory:** **PostgreSQL 16 + pgvector** (HNSW) for historical corpora, character knowledge, dialogue context.
- **Realtime:** WebSockets for AI streaming + state sync; multi‑user sessions with conflict resolution.
- **Assessments:** continuous evaluation → adaptive difficulty → **personalized learning paths**.
- **Integrations:** OAuth2/SAML SSO; **LTI 1.3** grade passback; xAPI/SCORM analytics.
- **Observability:** OpenTelemetry, Prometheus/Grafana, Sentry; SLA targets: **<300 ms AI**, **<5 s world load**.
- **Compliance:** FERPA/COPPA/GDPR data protection; RBAC + audit trails; PIIs encrypted at rest/in transit.

---
## 🧰 Core stack
- **Frontend (VR):** Unity 6+, OpenXR 1.12+, XR Interaction Toolkit, Addressables, URP
- **APIs:** FastAPI (Python 3.11+), Uvicorn/Gunicorn
- **Data:** PostgreSQL 16, **pgvector** 0.7+; Redis 7 (session/cache)
- **Infra:** Docker, Kubernetes/EKS, S3 + CloudFront (assets), Terraform + Ansible
- **CI/CD:** GitHub Actions (tests, FERPA checks, VR perf gates), container scanning
- **Auth:** OAuth2/SAML SSO (Auth0/AzureAD/Google), JWT for services
- **LMS:** LTI 1.3 (Canvas/Moodle/Blackboard/Google Classroom)

---
## 🚀 Quickstart (local dev via Docker)
> Minimal local stack for API/RAG work; the Unity VR client runs from the Editor.

```yaml
# docker-compose.yml (example)
services:
  postgres:
    image: pgvector/pgvector:pg16
    environment:
      POSTGRES_USER: gptco
      POSTGRES_PASSWORD: password
      POSTGRES_DB: gptco
    ports: ["5432:5432"]

  redis:
    image: redis:7
    ports: ["6379:6379"]

  # Optional: Qdrant if you prefer a separate vector store
  qdrant:
    image: qdrant/qdrant:v1.12.3
    ports: ["6333:6333"]

  # (Optional) Temporal for workflows
  temporal:
    image: temporalio/auto-setup:1.23
    environment:
      DB: postgresql
      POSTGRES_USER: gptco
      POSTGRES_PWD: password
      POSTGRES_SEEDS: postgres
    depends_on: [postgres]
    ports: ["7233:7233"]
```

### 1) Environment
```bash
cp .env.example .env
# set: OPENAI_API_KEY, DATABASE_URL, REDIS_URL, LMS_OAUTH, etc.
```

### 2) Run services
```bash
docker compose up -d
```

### 3) Launch APIs
```bash
# AI Teachers
uvicorn ai_teachers.app:app --reload --port 8080

# Assessment
uvicorn assessment.app:app --reload --port 8081
```

### 4) Unity client
- Install **Unity 6.x** with OpenXR + XR Interaction Toolkit.
- Open the `UnityProject/` folder, select **OpenXR** provider, enable target devices.
- Press **Play** to test in‑Editor; use device builds for on‑headset testing.

---
## 🧪 Quality gates (pre‑merge)
- **VR perf:** 90+ FPS; latency <20 ms motion‑to‑photon
- **AI:** p95 response <300 ms (streaming start); safety filters on
- **Data:** pgvector HNSW indexes; Prisma/SQLAlchemy migrations green
- **Compliance:** FERPA/COPPA checks; complete audit logs
- **LMS:** LTI 1.3 launch + grade passback integration tests

---
## 🔐 Privacy & Safety
- **PII encryption** (AES‑256 at rest, TLS 1.3 in transit); RBAC + row‑level security
- **Parental consent** & age gates for <13; minimal collection; export/erase tooling
- **Content safety** with educator override & logs

---
## 🗺️ Roadmap (excerpt)
- [ ] Classroom co‑present **25‑user** target with sub‑100 ms sync
- [ ] Educator dashboard (progress radars, cohort insights)
- [ ] World packs: Ancient Greece, Renaissance Italy, Abbasid Golden Age, Edo Japan
- [ ] Authoring tools: character kits + lesson templates
- [ ] Alt‑history scenarios (Phase 3), haptics, Vision Pro polish

---
## 🤝 Contributing
1. Fork + feature branch
2. Add tests (unit/VR play‑mode) and docs
3. Ensure quality gates pass
4. PR with context + demo clip/gif

---
## 📄 License
TBD — see `LICENSE` when available.
