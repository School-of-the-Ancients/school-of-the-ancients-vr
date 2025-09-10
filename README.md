# School of the Ancients (VR / Meta Horizon Worlds)

**A remixable VR museum where you can meet Cleopatra, Galileo, and Leonardo da Vinci.**  
Built in 48 hours for the Meta Horizon Worlds AI NPC Remix competition (2025).

---

## What It Is
Three themed zones (Egyptian plaza, hilltop observatory, beach workshop) with:
- AI NPCs + podium prompts (Yes/No/Tell me more + 3 custom questions each)
- Interactive props (Cleopatra’s scepter, Galileo’s telescope, Leonardo’s book)
- Global ocean ambience
- Intro/tutorial panel + credits/inspiration

Published world: https://horizon.meta.com/worlds/1459334171856325
Devpost: https://devpost.com/software/school-of-the-ancients

---

## Repo Contents
- `scripts/` — Desktop Editor TypeScript scripts (UI, NPC comms, events)  
- `docs/` — design notes, environment seeds/prompts, remix guide  
- `assets/` — optional QR images, etc.

> Note: You can’t export the world file itself. This repo provides everything needed to understand and remix the code/design.

---

## How to Remix (high level)
1. Open the world in **Horizon Worlds Desktop Editor**.  
2. Use the `CustomUI_*` scripts for the intro/podiums; `NpcCommunicator.ts` to trigger NPC responses.  
3. Swap meshes/props and update the prompt lists per figure.  
4. Bake and save your environment prefabs (Environment Gen → *Group* → *Save as Asset*) to avoid losing changes.  
5. Publish as **Public + Remixable**.

---

## Environment Generator Seeds
See `docs/environment-seeds.md` for the exact prompts/seeds used to rebuild the island and zone dressing.

---

## Roadmap
- Add more figures (Hypatia, Newton, Ada Lovelace)
- Light quest: “Ask me 3 things” unlocks a new exhibit
- Voice input once STT is exposed to creators
