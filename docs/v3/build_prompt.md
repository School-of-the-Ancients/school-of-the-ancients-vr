## WHY — VISION & PURPOSE

- **What problem are you solving and for whom?**\
  Traditional online courses struggle to keep attention, personalize difficulty, and show sources transparently. **School of the Ancients** solves this for **students (13+)**, **lifelong learners**, **educators/creators**, and **museums/schools** by turning lessons into **embodied, in‑character conversations** with **citation‑first** answers.

- **What does your application do?**\
  A **self‑managed VR academy**: AI teachers (historical and scientific figures) run **Socratic lessons**, adapt to learner knowledge, and cite sources. A **Matrix Operator** spawns rooms/props/assessments on command. Creators can publish and remix realms.

- **Who will use it?**

  - **Learners:** curious, mid/high‑school through adult, VR‑friendly.

  - **Creators/Educators:** teachers, museum docents, indie devs who want to build or remix worlds.

  - **Institutions:** schools and cultural orgs seeking immersive exhibits.

- **Why will they use it instead of alternatives?**

  - **Embodiment + agency**: learn *inside* the time/place.

  - **Socratic adaptivity** with visible **citations**.

  - **Operator speed**: build or modify lessons *during* class.

  - **Remixable and extensible** content packs.

---

## WHAT — CORE REQUIREMENTS

- **What must your application do?**

  - **System must** emulate selected figures with controllable persona, boundaries, and ethics.

  - **System must** ground responses in vetted sources and **surface citations**.

  - **System must** run **Socratic loops** with adaptive difficulty and mastery tracking.

  - **System must** expose **Operator** commands (voice/UI) for runtime world edits.

  - **Users must be able to** start sessions, answer checks, view progress, and request “Tell me more” or “Give me a hint.”

  - **Users must be able to** create/clone realms, add props, define lesson packs, and set access permissions.

  - **System must** support **sudo/admin** mode for creators (and restricted autonomous mode for AI under policies).

- **What actions need to happen?**

  - Select figure → load realm → run Q&A → inject props/media → assess → award mastery → suggest next lesson.

  - Creator: “new realm” → choose template → add figure → upload/choose sources → test lesson → publish.

  - Operator: spawn_asset, layout, attach_behavior, quiz.start, safety.freeze, save_scene.

- **What should the outcomes be?**

  - **Learner**: measurable knowledge gains, clear citations, badges/levels.

  - **Creator**: published realm with provenance and safety checks.

  - **Business**: growing library of high‑quality, remixable content; usage telemetry for improvement.

---

## HOW — PLANNING & IMPLEMENTATION

- **Required stack components**

  - **Frontend (VR):**

    - Track A (now): **Horizon Worlds** world + panels/UI.

    - Track B (port): **Unity (OpenXR, XR Interaction Toolkit)**; **Photon/Normcore** for multiplayer; **Ready Player Me** avatars (optional).

  - **Backend & AI:**

    - **OperatorServer** (FastAPI or Node) with HTTP/WS command contract.

    - **RAG**: **Supabase/Postgres** + vector embeddings over vetted texts (public‑domain translations + licensed sources).

    - **LLM** for in‑character tutoring with **citation injection**; **policy layer** (safety, age‑gating, persona limits).

    - **STT/TTS** provider(s); **content moderation** and **profanity/harassment filters**.

  - **Infra:**

    - Containerized services; telemetry & logs; feature flags; nightly content validation.

    - CDN/object storage for lesson assets.

- **System requirements**

  - **Performance:** &lt;150 ms local Operator command echo; &lt;1.5 s NPC first‑token; 72/90Hz VR frame budget.

  - **Security:** role‑based access; audit logs for sudo; PII minimization; COPPA/FERPA awareness for edu pilots.

  - **Scalability:** stateless OperatorServer, horizontal scaling; vector DB sharding by collection.

  - **Reliability:** 99.5% uptime target for Operator/LLM endpoints; autosave scenes every 2 min.

  - **Integration constraints:** Horizon builds follow platform limits; Unity port respects OpenXR device targets.

- **Key user flows**

  1. **Learn a lesson**: Home → Pick figure → Enter realm → Teacher greets → Q&A loop (with props) → 3–5 checks → mastery % + sources → next suggestion.

  2. **Create a realm**: New realm → Template → Add figure → Upload/select sources → Generate lesson pack → Playtest → Publish.

  3. **Operator live edit**: Voice/panel → spawn_asset/layout/quiz.start → students experience changes live → save snapshot.

  4. **Assess & review**: View dashboard → drill into wrong answers → spaced repetition schedule.

- **Core interfaces**

  - **Student HUD**: prompt bubble, “Why?”, “Hint”, “Show source”, progress ring, pause.

  - **Teacher Panel** (creator): persona sliders (tone, depth), content scope, safety toggles, “Test lesson.”

  - **Operator Console**: command list, logs, undo, freeze, save.

  - **Library**: figures, realms, lesson packs with provenance badges.

---

## BUSINESS REQUIREMENTS

- **Access & authentication**

  - Roles: **Student**, **Creator/Teacher**, **Operator (Admin)**, **Autonomous AI (restricted)**.

  - Auth: platform SSO (Meta account) for Horizon; OAuth for Unity build; optional classroom codes.

  - Access control: per‑realm permissions; sudo requires explicit grant + logs; AI sudo only within sandboxed commands.

- **Business rules**

  - **Citations first** for any fact; provide link/snippet where possible.

  - Prefer **public‑domain** texts; license modern translations and media when required.

  - **No impersonation of living persons** without rights/consent; use “inspired‑by” personas instead.

  - **Age gates** and safe‑content filters; session recording disabled by default for minors.

  - **Latency budgets** must be met before publishing a realm.

  - **Service levels:** Operator/LLM 99.5% uptime; critical bug fix SLA 72h in beta.

- **Implementation priorities**

  - **High:** Socratic Q&A + citations; Operator core (spawn_asset/layout/quiz.start/save); 3 starter realms (Cleopatra, Galileo, Leonardo); mastery checks; creator publishing; safety layer.

  - **Medium:** Voice I/O end‑to‑end; cohort mode; dashboard & spaced repetition; provenance badges.

  - **Lower:** Marketplace, achievements/badges gallery, advanced animation passes, multi‑scene quests.