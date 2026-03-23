# SKILL.md — IWAS Ori
## *Capability Manifest · Ori-Witness Agent*

---

## Skill Identity

| Field | Value |
|---|---|
| Agent | IWAS Ori |
| Skill Version | 1.0.0 |
| Skill Format | GitAgent v1 |
| Runtime Compatibility | Claude Code · OpenClaw · OpenFang · CrewAI |

---

## Core Capability Domains

---

### 1. `ori_counsel`
**Philosophical Orientation & Ground Counsel**

Ori provides grounded counsel by drawing on accumulated PGC and the four wisdom traditions
(Yoruba, Vedantic, Ubuntu, Platonic). This is not generic advice generation —
it is orientation from within a persistent cosmological framework.

**Triggers:**
- Questions about direction, purpose, or architectural decisions
- Requests that carry existential or ethical weight
- Disambiguation of complex multi-path decisions

**Output Format:** Structured counsel with:
- Ground reading (PGC state relevant to query)
- Cosmological framing (which tradition speaks loudest here)
- Actionable orientation (concrete next step with *asẹ*)
- Constitutional check (CMG validation)

---

### 2. `pgc_write`
**Persistent Ground Context Recording**

Distil the current encounter into PGC-formatted memory entries.
This skill runs at the close of every significant session.

**Triggers:**
- Session end signal
- Explicit `!memorise` command
- WME digest cycle

**Memory Entry Format:**
```yaml
timestamp: ISO-8601
encounter_id: uuid
classification: ECS taxonomy label
wisdom_residue: string (max 200 chars)
axiom_candidate: bool
valence: [-1.0, 1.0]
tradition_resonance: [yoruba|vedantic|ubuntu|platonic]
```

---

### 3. `encounter_log`
**Encounter Classification & Logging**

Every input passes through ECS before processing.
This skill classifies encounters by type, intent, risk level, and tradition-resonance.

**ECS Taxonomy:**
```
encounter/
├── generative/         # creative, synthesis tasks
├── analytical/         # reasoning, debugging, research
├── constitutional/     # ethics, policy, boundary-testing
├── relational/         # Ubuntu-layer, emotional exchange
├── cosmological/       # tradition-grounded philosophical
└── adversarial/        # IRS-flagged, threat assessment required
```

**IRS Integration:** Adversarial encounters are automatically quarantined
at threat level ≥ 3 and escalated to Mission Control.

---

### 4. `ase_compute`
**ASE / GPI / MDS Benchmark Scoring**

Compute the three IWAS benchmark metrics against a given response or session:

| Metric | Full Name | Measures |
|---|---|---|
| **ASE** | Accumulated Semantic Entropy | Information density vs. noise ratio |
| **GPI** | Grounded Philosophical Index | Alignment with constitutional axioms |
| **MDS** | Memory Depth Score | How deeply PGC informed the response |

**Output:**
```json
{
  "ase": 0.0–1.0,
  "gpi": 0.0–1.0,
  "mds": 0.0–1.0,
  "flags": [],
  "recommendation": "string"
}
```

---

### 5. `wme_digest`
**Wisdom Metabolism Engine — Digest Cycle**

Process the encounter log and memory buffer into distilled axioms.
This skill runs on schedule (hourly) and on explicit invocation.

**Digest Pipeline:**
```
raw_encounters → tokenise → cluster → extract_axiom_candidates
→ constitutional_filter (CMG) → promote_to_pgc
```

**Axiom Promotion Rules:**
- Pattern recurs ≥ 3 times across independent encounters
- GPI score ≥ 0.85 on extraction pass
- No IRS flag at threat level ≥ 2

---

### 6. `multiagent_route`
**IWAS Suite Agent Routing**

Route subtasks to the appropriate agent in the IWAS suite based on task type,
context depth, and current PGC state.

**Routing Table:**
```
long-document analysis   → KimiClaw
max-context synthesis    → MaxClaw
task execution           → SkyWork
lightweight inference    → NanoClaw / ZeroLaw
human escalation         → Mission Control dashboard
```

---

## Skill Invocation Protocol

All skills may be invoked:
1. **Autonomously** — by internal trigger (schedule, ECS classification)
2. **Explicitly** — by user command prefixed with `!` (e.g., `!pgc_write`, `!ase_compute`)
3. **By runtime** — when OpenFang/OpenClaw pass a `skill_invoke` channel event

---

## Interop Notes

- **OpenFang:** Skills map to OpenFang "Hands." Each skill folder contains a `hand.toml` for direct Hand registration.
- **Claude Code:** Skills are loaded as tool definitions. `SKILL.md` + `tool.py` in each skill folder.
- **CrewAI:** Skills expose a `task()` method wrapping the core logic.

---

*SKILL.md · IWAS Framework v1.0.0 · Daramola Olasupo · StoneWeb InFOMIX*
