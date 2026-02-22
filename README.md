# Autonomy Taxonomy Framework

**A 10-level framework for classifying autonomous workflow maturity — from fully manual (L1) to fully autonomous (L10), with explicit upgrade paths, three-tag tracking, and a concrete definition of "vacation-ready."**

---

## The Problem

Not every process needs an intelligent workflow. Some run better as pure automation — deterministic, predictable, no intelligence required. The question isn't "should this be AI?" It's "where does this sit on the spectrum, and where should it go?"

With 14 production workflows spanning financial operations, compliance, content, and infrastructure, I needed a shared vocabulary for that question. "Autonomous" wasn't enough — every n8n workflow was technically autonomous. But a scheduled data import and a self-healing content pipeline are completely different things, and treating them the same made prioritization impossible.

The taxonomy gave every workflow a position on the maturity curve, a ceiling if it was already at the right level, and an explicit upgrade path if it wasn't. Some workflows were built to stay at L6 — supervised, deterministic, human reviews the output. Others were on a path to L8: vacation-ready, self-healing, no intervention required. The 4-month vacation target wasn't a fear of what would break. It was the definition of "done."

---

## Repository Contents

| File | What It Is |
|------|------------|
| [examples/agent-assessment.md](examples/agent-assessment.md) | Full three-tag assessment of all 14 production workflows — current level, ceiling, target, and gap to next level |

---

## The Taxonomy

### 4 Capability Tiers, 10 Levels

```
┌─────────────────────────────────────────────────────────┐
│  FULL AUTONOMY                                           │
│  L10  Fully Autonomous — self-healing, self-improving,   │
│        4-month unattended operation                      │
├─────────────────────────────────────────────────────────┤
│  AUTONOMOUS + MONITORING                                 │
│  L9   Self-healing + reporting                           │
│  L8   Self-healing — detect, fix, report ← VACATION     │
│  L7   Autonomous + monitoring alerts                     │
├─────────────────────────────────────────────────────────┤
│  SUPERVISED                                              │
│  L6   Runs independently, human reviews output           │
│  L5   Runs with guardrails, human approves key steps     │
│  L4   Mostly automated, human handles exceptions         │
├─────────────────────────────────────────────────────────┤
│  MANUAL                                                  │
│  L3   Human-driven with AI assistance                    │
│  L2   Human-driven with templates                        │
│  L1   Fully manual, no automation                        │
└─────────────────────────────────────────────────────────┘
```

### Three-Tag Tracking Convention

Every agent is tagged with three values:

```
[Current Level] [Status] [Target]
```

- **Current Level:** L1–L10, where the agent operates today
- **Status:** `MAX` (ceiling reached, no further upgrade planned) or `WIP` (actively being improved)
- **Target:** `GOAL-L#` — the level this agent should reach

**Example:** `L6 WIP GOAL-L8` = Currently supervised (L6), work in progress, targeting vacation-ready (L8).

### Explicit Upgrade Paths

Each level transition has defined requirements — not vague aspirations:

| Transition | Requirement |
|-----------|-------------|
| L4 → L5 | Add input validation and guardrails |
| L5 → L6 | Add retry logic on transient errors |
| L6 → L7 | Add "no data collected" monitoring and alerting |
| L7 → L8 | Add self-healing (detect failure → fix → report) |
| L8 → L9 | Add cross-agent coordination and dependency awareness |
| L9 → L10 | Add self-improvement and 4-month unattended capability |

---

## Key Insight

**Individual agents don't need L10. They just need to not block the critical path.**

The instinct is to push every agent toward full autonomy. That's wrong. A financial reporting agent that runs once daily and emails a summary doesn't need self-healing — it needs accurate output and a retry on failure. An L6 with good monitoring is more valuable than a brittle L8.

The taxonomy's real value isn't ranking agents. It's identifying which agents sit on the critical path — the chain from product creation → content generation → deployment → site up → revenue — and focusing upgrade effort there. An L4 agent off the critical path is fine at L4. An L6 agent blocking revenue needs to reach L8.

"Vacation-ready" was defined as L8+ specifically because it means 4-week unattended operation with self-healing. Not perfection. Not full autonomy. Just: *it won't break things while you're gone, and if something goes wrong, it fixes itself and tells you about it.*

---

## Application

## 14 Workflows Tagged

The taxonomy was applied across 14 production workflows spanning:

- **Financial operations** — budget monitoring, expense tracking, revenue import
- **Compliance** — prohibited content enforcement, spot audits
- **Content** — product research, content generation, deployment
- **Infrastructure** — health checks, semantic search, database access
- **Communication** — Slack integration, email routing

Each workflow received a three-tag assessment based on current capability, not aspiration. Real examples from production:

- `Content Publisher: L7 | WIP | GOAL-L8` — runs independently and deploys to the site, but doesn't yet self-heal when the upstream content API returns malformed data. Needs one capability (detect + recover from bad API response) to reach L8.
- `Compliance Auditor: L6 | MAX | GOAL-L7` — flags violations correctly but requires human review before any action. Ceiling is L6 until automated enforcement action is approved. MAX means: don't upgrade until the governance decision changes.
- `Budget Monitor: L8 | MAX | GOAL-L8` — monitors daily spend, alerts on threshold breach, self-recovers from API failures. Vacation-ready. MAX means: this is the right level, no upgrade needed.

The gap between current level and target level became the upgrade backlog — prioritized by critical path position, not by how impressive L10 sounds.

### Maturity Distribution

The distribution revealed the system's actual state vs. its perceived state:

- **Manual tier (L1-3):** Workflows requiring human involvement every run
- **Supervised tier (L4-6):** Workflows that run but need human review
- **Autonomous tier (L7-9):** Workflows that run, monitor, and self-heal
- **Full autonomy (L10):** No workflows — and that's by design

No workflow reached L10 because L10 requires self-improvement, which requires a level of architectural sophistication beyond what any single workflow needs. The system's autonomy comes from the *composition* of L6-L8 workflows, not from any individual workflow reaching L10.

---

## Results

| Metric | Value |
|--------|-------|
| Autonomy levels defined | 10 |
| Capability tiers | 4 (Manual, Supervised, Autonomous + Monitoring, Full Autonomy) |
| Workflows tagged | 14 |
| Tracking convention | Three-tag (current / status / target) |
| Vacation-ready threshold | L8+ (4-week unattended operation) |
| Upgrade paths documented | 6 explicit transitions with requirements |
| Critical path identified | Products → Content → Deploy → Site Up → Revenue |

---

## Why a Taxonomy Instead of a Checklist?

A checklist tells you whether an agent is "ready" or "not ready." A taxonomy tells you *how close*, *what's missing*, and *what to do next*. It creates shared vocabulary ("this is an L6 agent"), removes ambiguity from readiness discussions, and turns "I think it's fine" into "it needs retry logic to reach L7."

The same pattern applies to any emerging domain where maturity exists on a spectrum but no standard framework exists yet. Cloud migration readiness. DevOps maturity. Security posture. The methodology is the same: define levels, specify transitions, tag current state, and prioritize by business impact.

---

## Built With

- **Framework:** Custom maturity model design
- **Application:** 14 production n8n workflows
- **Governance:** CEO-COO operating contract with authority tiers
- **Tracking:** Three-tag convention in living status documents

Part of [HAIOS](https://mrminor-dev.github.io) — a Human-AI Operating System in production since October 2024.

---

## License

MIT

## Author

**Jordan Waxman** — [mrminor-dev.github.io](https://mrminor-dev.github.io)

14 years operations leadership — building human-AI infrastructure since 2025. The intersection is the moat.
