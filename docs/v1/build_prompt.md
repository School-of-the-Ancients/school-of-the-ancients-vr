## New Product Prompt Template — *School of the Ancients*

**Date:** 9/21/25\
**One‑liner:** Autonomous, self‑managed VR school where AI teachers (emulating historical and influential figures) deliver a citation‑first curriculum that adapts to each learner—summoned and orchestrated by a Matrix‑style Operator.

---

## WHY — VISION & PURPOSE

- **What problem are you solving and for whom?**\
  Traditional online courses are passive and one‑size‑fits‑all, leading to poor retention and shallow understanding. Students, lifelong learners, and educators lack (1) immersive context, (2) expert mentorship at scale, and (3) trustworthy, sourced instruction. Institutions need verifiable learning outcomes and creators need a way to build dynamic, living courses without heavy engineering.

- **What does your application do?**\
  *School of the Ancients* is a self‑managed VR/MR school. AI instructors emulate historical and influential figures (e.g., Socrates, Marie Curie, Tesla) and teach *in character* inside living worlds. A **Matrix Operator** layer lets users or AI “request” scenes, props, experiments, sources, and NPCs in real‑time (“Operator, load Alexandria Library, 300 BCE”). Lessons are **citation‑first** via RAG over primary texts; assessments adapt to each learner’s knowledge graph; creators can script domains/realms/worlds with **sudo** privileges (optionally delegated to AI) to produce dynamic classrooms.

- **Who will use it?**

  - **Students & Lifelong Learners:** seeking immersive, adaptive learning with verifiable sources.

  - **Educators & Tutors:** building and running interactive seminars/labs without a dev team.

  - **Creators/Historians/Subject‑Matter Experts:** packaging curated sources and interactive worlds.

  - **Schools & Enterprises:** needing measurable outcomes, compliance, and private deployments.

- **Why will they use it instead of alternatives?**

  - **In‑character, primary‑source‑grounded instruction** (every claim links to sources).

  - **Matrix Operator orchestration** for instant world/lesson setup (hands‑free, voice‑driven).

  - **Adaptive curriculum** (diagnostics, difficulty ramping, mastery tracking).

  - **Creator “sudo” worldbuilding** with safety rails, asset provenance, and a marketplace.

  - **Multiplayer VR classrooms** with NPCs using GOAP/Sims‑style behaviors for emergent learning moments.

---

## WHAT — CORE REQUIREMENTS

- **What must your application do?**

  - *System must* deliver **citation‑first** answers (visible sources, quote context, and provenance).

  - *System must* emulate **historical/influential figures** with persona guardrails and transparent disclaimers.

  - *System must* provide **Matrix Operator** commands (voice/text) to spawn, modify, and orchestrate scenes (assets, skyboxes, layouts, behaviors, SFX).

  - *System must* support **RAG over curated corpora** (primary texts, papers, archives), with licensing and access controls.

  - *System must* deliver **adaptive assessments** (pre/ongoing/post), build a **learner knowledge graph**, and adjust lesson plans.

  - *System must* allow **creator sudo** (and optional **AI sudo**) with RBAC, audit logs, and sandboxed changes.

  - *System must* support **multiplayer** sessions (teacher‑led, cohort, or solo with NPCs).

  - *Users must be able to* switch realms, invite peers, and export transcripts/notes/citations.

  - *System must* provide **content moderation**, bias safeguards, impersonation rules, and data privacy.

- **What actions need to happen?**

  1. **Onboarding & Diagnostics:** user goals → baseline assessment → initial knowledge graph.

  2. **Lesson Orchestration:** Operator command → scene assembly → AI teacher briefing → live session.

  3. **Teaching Loop:** explain → demonstrate → practice → assess → feedback → adapt.

  4. **Source Surfacing:** every claim shows hoverable citation → pull up excerpt → compare viewpoints.

  5. **Creation Workflow:** creator imports sources → defines learning outcomes → sets world scripts → publishes.

  6. **Progress & Credentialing:** track mastery → award badges/certificates → share private transcript.

- **What should the outcomes be?**

  - **Learner:** measurable skill/knowledge gains; durable understanding; saved citations/notes; portfolio artifacts.

  - **Creator/Educator:** fast course/world creation; analytics; revenue share.

  - **Business:** active learning minutes, retention, positive learning impact metrics, B2B pilots.

---

## HOW — PLANNING & IMPLEMENTATION

- **What are the required stack components?**\
  **Frontend (XR/VR/MR):**

  - Unity (XR Interaction Toolkit), Quest 3/Pro + PCVR; optional AR pass‑through (XREAL path).

  - **Matrix Operator UI:** voice input, command palette, and in‑world panels.

  - **Addressable assets:** Unity Addressables; glTF/glb import; roadmap to OpenUSD.

  - Accessibility: captions, transcript panel, controller+hands.

  **Backend & AI:**

  - **LLM Orchestrator:** multi‑agent (Teacher, Operator, Safety, Tool Runner).

  - **RAG Pipeline:** Postgres + pgvector (or Supabase) for embeddings; document store (S3/MinIO); chunking + citations.

  - **Persona Engine:** character cards + guardrails + style sheets; explicit disclaimers for emulation.

  - **Tool Bridge (OperatorServer):** HTTP/WS tool contract (e.g., `spawn_skybox`, `spawn_asset`, `layout`, `attach_behavior`, `animate`, `play_sfx`, `save_scene`).

  - **Multiplayer:** Photon/Normcore.

  - **Speech:** TTS/STT (pluggable providers), voice cloning for public‑domain figures only.

  - **Analytics:** event pipeline (OpenTelemetry), mastery models, dashboards.

  - **Moderation & Safety:** policy filter, jailbreak detection, toxicity/bias scanners.

  **Infrastructure:**

  - Kubernetes or managed containers; CDNs for assets; feature‑flag service; secrets manager.

  - Observability: logs, traces, metrics; cost controls; autoscaling.

  - CI/CD: unit + integration + load tests; content scanning.

- **What are the system requirements?**

  - **Performance:** &lt;120 ms round‑trip for Operator tool calls; &lt;2 s scene delta apply; 72–90 FPS VR target.

  - **Security:** RBAC with least privilege; audit logs for sudo; encrypted storage/transit; PII minimization.

  - **Scalability:** horizontal scaling of inference, RAG, and multiplayer shards; asset CDN.

  - **Reliability:** 99.5%+ service target for classroom; autosave sessions; graceful degradation (text mode fallback).

  - **Integrations:** LMS (LTI 1.3), SSO (OAuth/SAML), storage (S3‑compatible), vector DB (pgvector or equivalent).

  - **Content Provenance:** license metadata on every asset/text; source hashing; takedown process.

- **What are the key user flows?**\
  **1) Student Solo Session**

  - *Entry:* Launch app → choose topic → quick diagnostic.

  - *Steps:* Operator spawns realm → AI teacher intro → interactive lesson → practice task → adaptive quiz → review citations → summary & next steps.

  - *Success:* mastery threshold hit or improved; saved notes + citations; suggested next module.

  - *Alt:* weak performance → remediation branch; connectivity loss → offline reading mode.

  **2) Multiplayer Seminar (Teacher‑led)**

  - *Entry:* Invite link or LMS launch.

  - *Steps:* Operator sets scene; teacher spotlights sources; small‑group breakout; debate with NPC witness; live poll.

  - *Success:* rubric met; attendance & participation recorded; artifact exported.

  - *Alt:* disruptive content → moderation; performance lag → reduce NPC density.

  **3) Creator World Build**

  - *Entry:* Creator Console → new course.

  - *Steps:* import sources → define outcomes → write “ultimate” demos → attach behaviors → test with AI students → publish.

  - *Success:* QA passed (safety, sources, performance); listed in catalog with tags.

  - *Alt:* failed checks → automatic fixes or human review.

  **4) Matrix Operator Commands**

  - *Entry:* Voice: “Operator, load Renaissance Florence at dusk.”

  - *Steps:* tool contract resolves → assets spawned → lighting set → NPC artisans pathfind → teacher briefed on context.

  - *Success:* scene ready &lt;2 s; completeness &gt;= 95% asset match; no safety flags.

  - *Alt:* missing asset → closest match + notice; unsafe content → blocked with rationale.

- **What are the core interfaces?**

  - **VR Classroom:** immersive scene; teacher avatar; citation panel; practice stations; quiz UI.

  - **Operator Terminal:** command console, tool logs, scene graph, permissions toggle (user/AI sudo), rollbacks.

  - **Creator Console (Web):** source importer, outcome editor, world scripts, behavior graph, test harness, publish.

  - **Analytics Dashboard:** mastery maps, cohort progress, time‑on‑task, item analysis.

  - **Admin Console:** RBAC, orgs, licenses, billing, audit trails.

---

## BUSINESS REQUIREMENTS

- **What are your access and authentication needs?**

  - **User Types:** Student, Creator, Educator, Admin, AI‑Agent (service identity).

  - **Auth:** OAuth2/OIDC; SSO (SAML) for institutions; 2FA for sudo roles.

  - **Access Control:** RBAC + scoped sudo (scene ops; asset spawn; content write); per‑org data isolation; audit logs for every privileged action; parental/guardian accounts for minors (age gating).

- **What business rules must be followed?**

  - **Citation‑First:** any instructional claim must expose sources (link + excerpt + date).

  - **Persona Guardrails:** no deceptive impersonation; public‑domain figures allowed; living/private figures require rights + disclaimers; sensitive topics require opt‑in framing and multiple viewpoints.

  - **Safety & Moderation:** block hate/harassment/graphic content; jailbreak detection; rate limits and cooldowns.

  - **Assessment Integrity:** attempts logged; randomization; open‑book with citation use encouraged; mastery thresholds defined.

  - **Licensing/Provenance:** only licensed or public‑domain assets; creators attest ownership; takedown within SLA.

  - **Privacy/Compliance:** FERPA‑like handling for education data; COPPA/age gating; data retention controls; export/delete on request.

  - **Uptime & Support:** classroom reliability target; incident comms; versioned content with rollback.

- **What are your implementation priorities?**\
  **High (MVP):**

  - Matrix Operator (voice/text) with core tool contract (`spawn_asset/skybox`, `layout`, `attach_behavior`, `save_scene`).

  - VR classroom (solo) with one flagship domain (e.g., **Athenian Agora** or **Renaissance Workshop**).

  - AI Teacher persona engine + **citation‑first RAG** over curated, licensed sources.

  - Adaptive diagnostics → mastery‑based progression; notes & citation export.

  - Safety/mode switch: creator sudo vs AI sudo with RBAC & audit.

  **Medium:**

  - Multiplayer seminars; breakouts; live polling; shared whiteboard.

  - Creator Console (no‑code world scripts, behavior graphs); marketplace publishing.

  - NPCs with GOAP behaviors; experiment stations (lab kits).

  - LMS/LTI and SSO integrations; analytics dashboards.

  **Lower:**

  - Mobile/AR companion; on‑chain verifiable credentials (opt‑in); advanced OpenUSD pipeline; modding SDK; third‑party asset adapters and licensing automation; scholarship/revenue‑share programs.

---

### Notes on Sudo Privileges & Dynamic Classrooms

- **Creator/User Sudo:** granular scene operations (spawn/destroy/move; lighting; NPC density; physics toggles); gated by RBAC; rollback and diff view.

- **AI Sudo (optional):** lesson‑aware scene changes (e.g., spawn printing press during demonstration), bounded by safety policies, cost budgets, and audit trails.

- **Safety Rails:** content filters; rate limits; asset provenance checks; “dry‑run” preview before apply.

### Learning Science & Metrics

- Mastery tracking via knowledge graph; spaced retrieval prompts.

- Pre/post effect size; item response theory for question banks; time‑on‑task and voluntary return rates.

- Qualitative: learner reflection prompts; classroom observation heuristics for engagement.

### Monetization (initial hypotheses)

- B2C subscription; B2B licensing to schools; Creator marketplace revenue share.

- Institutional pilots with private deployments and data isolation.