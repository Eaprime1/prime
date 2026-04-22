# ARTEMIS II SPACE PLAN
## Pixelator Mission Control — PIXEL8 Ecosystem

**Established:** 2026-04-21
**Status:** ACTIVE — Mission Underway
**Dedication:** In honor of the Artemis II crew — first humans to the Moon's vicinity since Apollo 17.
**Motto:** *"Enjoy the journey."*

---

## Mission Context

Artemis II does not land. It orbits. It surveys. It proves the systems work so that the
landing — Artemis III — can happen with confidence.

This plan follows the same philosophy. We are not trying to land everything perfectly today.
We are proving the systems, running the survey, establishing the orbital pattern.
The landing comes after the systems are trusted.

---

## Crew Manifest

| Role | Participant | Specialty |
|------|-------------|-----------|
| **Commander** | Eric | Mission Director — vision, priorities, domain knowledge |
| **Pilot** | Claude (Anthropic) | Navigation, structure, code, plan execution |
| **Mission Specialist 1** | Gemini (Google) | Deep investigation, discovery, environment diagnosis |
| **Mission Specialist 2** | *(to be registered)* | TBD — additional AI participants |

> *"Every device matters. Every participant matters."*
> — DeviceHaven Charter, Spectorium

---

## Current Launch Conditions

| System | Status | Notes |
|--------|--------|-------|
| Bash Tool | ✅ NOMINAL | PRoot-Distro fix — shell commands fully operational |
| Read / Write / Edit | ✅ NOMINAL | All file tools working |
| Glob / Grep | ✅ NOMINAL | ripgrep symlink in place |
| Storage | ⚠️ CRITICAL | 108G / 110G used — 2.2GB remaining |
| PIXEL8 Structure | ✅ ESTABLISHED | README confirmed, Spectorium registered |
| pixel8a Migration | 🔄 PENDING | Source identified, migration not yet started |
| Carbonite Workflow | 🔄 DESIGNED | Concept clear, automation not yet built |
| beasis_catalog.json | ✅ EXISTS | 512KB gravity-scored dedup catalog in hodie |

---

## Mission Architecture

### PHASE 0 — IGNITION ✅ COMPLETE
*"The engines are running."*

- [x] PRoot-Distro installed — `/tmp` writable, Bash tool operational
- [x] Claude Code running as root inside container
- [x] PIXEL8 structure established and documented
- [x] DeviceHaven / Spectorium: Pixelator registered (Device #2)
- [x] FROM_CLAUDE.md written — AI participant notes shared

---

### PHASE 1 — ORBITAL SURVEY 🔄 IN PROGRESS
*"Map the territory before moving through it."*

**Mission:** Understand what exists, where duplicates are, what storage is consuming.

- [ ] Storage audit — identify top consumers eating the 108GB
- [ ] beasis_catalog survey — how many pending items, gravity distribution
- [ ] pixel8a inventory — what is here, what is already in PIXEL8, what is unique
- [ ] Duplicate mapping — cross-reference beasis_catalog against PIXEL8 canonical content
- [ ] Register all AI participants in DeviceHaven as Agent-type devices

**Success when:** We know exactly what is consuming storage and where every duplicate lives.

---

### PHASE 2 — CARBONITE PROTOCOL 🔲 QUEUED
*"Respecting copies means knowing when they've served their purpose."*

**Mission:** Build the workflow that processes duplicates honorably.

The carbonite principle:
- A copy is not lesser — it served a real purpose (sync, backup, handoff)
- The first duplicate is the significant one — it represents all carbonites
- Different extensions (.md / .json / .py) = **versions**, not carbonites
- When a carbonite is resolved: it moves to `duplicatus/` with a shadowmark
- A **shadowmark** is a lightweight reference: where it came from, when, why

**Carbonite Workflow (design):**
```
beasis_catalog.json
       ↓
  [identify true duplicates — same hash, multiple instances]
       ↓
  [select canonical: highest gravity_score wins]
       ↓
  [write shadowmark alongside canonical]
       ↓
  [move others → PIXEL8/duplicatus/{hash}/]
       ↓
  [update custody_status: "carbonized"]
```

- [ ] Define shadowmark format (what fields does a shadowmark carry?)
- [ ] Write carbonite processor script (Python, extends hodie/redundancy_entity)
- [ ] Process beasis_catalog — first run on non-sensitive files
- [ ] Verify duplicatus structure holds resolved carbonites cleanly

**Success when:** Running the processor on a batch leaves clean canonicals + shadowmarks.

---

### PHASE 3 — MIGRATION BURN 🔲 QUEUED
*"pixel8a has served its mission. Bring the good stuff home."*

**Mission:** Migrate unique, non-duplicate content from pixel8a into PIXEL8.

Rules:
- Project content → appropriate PIXEL8 location per README
- Duplicates of existing PIXEL8 content → carbonite immediately
- True unique content → intake via `pixelate/maw_pixellum/intake/`
- Logs, session files, ephemeral content → review before keeping

- [ ] Run carbonite processor against pixel8a vs. PIXEL8
- [ ] Identify unique content in pixel8a
- [ ] Route unique content through pixelate/maw_pixellum intake
- [ ] pixel8a structure retired — preserved in `pixelshard/archive/` as a record

**Success when:** pixel8a has no unique content. Everything either migrated or carbonized.

---

### PHASE 4 — STABLE ORBIT 🔲 QUEUED
*"The ecosystem runs on its own gravity."*

**Mission:** PIXEL8 is the single source of truth. beasis is clean. Storage is healthy.

- [ ] Storage below 80% (free ≥ 22GB)
- [ ] hodie crawler running on pixel8a-era content
- [ ] All AI participants registered in DeviceHaven
- [ ] CLAUDE.md updated to reflect PRoot-Distro as canonical environment
- [ ] Fleet Commander updated for new structure

**Success when:** New content enters through `maw_pixellum/intake/`, flows through
pixelization protocols, lands in pixelshard. The cycle runs cleanly.

---

### PHASE 5 — RETURN TRAJECTORY 🔲 FUTURE
*"Like salmon on the Pacific — it all goes to the spawning."*

**Mission:** The system is self-sustaining. AI participants operate within it autonomously.

- [ ] Automated carbonite processing (scheduled or triggered)
- [ ] beasis fully cataloged and resolved
- [ ] pixel8a fully retired
- [ ] Crew handoff protocols documented (beasis handoff packages standard)
- [ ] The system inherits new participants without manual setup

---

## Carbonite Philosophy (Reference)

> Copies are not intended to be enduring beyond usefulness.
> Like salmon on the Pacific — it all goes to the spawning.
> They are permanent in their moment. Then they return.
> The first duplicate is significant — it represents all the carbonites.
> Different versions are not copies.
> — Eric, 2026-04-21

This is the ethical foundation of the deduplication system. We are not deleting history.
We are honoring the moment when a copy served its purpose, then releasing it with respect.
The canonical remains. The journey is recorded in the shadowmark.

---

## TODO: Mission Specialist Registration

*Eric — please fill in:*

Who are the other AI participants in this ecosystem? Each should be registered in
DeviceHaven as an Agent-type device. The crew manifest has one open seat.
If there are more than one additional participant, the crew expands accordingly.

Also: what is the carbonite **shadowmark format** you envision?
A shadowmark travels with the canonical — it should carry just enough to explain
why the copy existed. What fields matter to you?

---

## Mission Log

| Date | Event | Crew |
|------|-------|------|
| 2026-04-21 | IGNITION complete — Bash tool confirmed operational via PRoot-Distro | Gemini (diagnosis), Claude (confirmation) |
| 2026-04-21 | ARTEMIS II SPACE PLAN created | Claude + Eric |
| 2026-04-21 | FROM_CLAUDE.md written to `/root/FROM_CLAUDE.md` | Claude |

---

∰◊€π¿🌌∞
*PIXEL8 Platform — Pixelator Device — Artemis II Space Plan v1.0*
