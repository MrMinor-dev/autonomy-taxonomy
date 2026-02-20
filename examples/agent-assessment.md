# Agent Assessment — 14 Production Workflows

Full three-tag assessment applied across all 14 production workflows. Each tag: `[Current Level] [Status] [Target]`

- **Current Level:** Where the workflow operates today (L1–L10)
- **Status:** `MAX` = at the right level, no upgrade planned | `WIP` = actively being improved
- **Target:** The level this workflow should reach

The ceiling isn't always L10. Some workflows are better as pure n8n automation — deterministic, predictable, at L6 or L7 by design. MAX means: this is the right level for this workflow, given what it does and where it sits on the critical path.

---

## Financial Operations

| Workflow | Tag | What It Does | Gap to Target |
|----------|-----|--------------|---------------|
| Budget Monitor | `L8 MAX GOAL-L8` | Monitors daily spend, alerts on threshold breach, self-recovers from API failures | At target. Vacation-ready. |
| Expense Tracker | `L6 WIP GOAL-L8` | Categorizes transactions, flags anomalies for review | Needs: auto-confirm high-confidence categorizations (→L7), self-heal on upstream API changes (→L8) |
| Revenue Import | `L7 WIP GOAL-L8` | Imports daily revenue data, retries on transient failures, alerts on missing data | Needs: detect and recover from upstream format changes without human intervention |

## Compliance

| Workflow | Tag | What It Does | Gap to Target |
|----------|-----|--------------|---------------|
| Content Compliance | `L8 MAX GOAL-L8` | Enforces prohibited content rules pre-publish, blocks violations, logs audit trail | At target. No human approval required. |
| Compliance Auditor | `L6 MAX GOAL-L6` | Spot-audits published content, flags violations, surfaces for human review | Ceiling is L6 until automated enforcement action is approved. MAX = governance decision, not capability gap. |

## Content

| Workflow | Tag | What It Does | Gap to Target |
|----------|-----|--------------|---------------|
| Product Research | `L5 WIP GOAL-L7` | Scrapes product data, validates schema, queues for content generation | Needs: retry on malformed data (→L6), monitoring alert on queue stall (→L7) |
| Content Generator | `L7 WIP GOAL-L8` | Generates product content, self-validates quality, retries on failure | Needs: detect and recover from upstream API returning malformed responses |
| Content Publisher | `L7 WIP GOAL-L8` | Deploys approved content to site, confirms successful publish | Needs: self-heal when upstream content API returns unexpected format |

## Infrastructure

| Workflow | Tag | What It Does | Gap to Target |
|----------|-----|--------------|---------------|
| Health Monitor | `L8 MAX GOAL-L8` | Checks all critical services daily, routes alerts by severity, self-recovers from check failures | At target. Vacation-ready. |
| Semantic Search | `L7 MAX GOAL-L7` | Processes queries, returns ranked results, alerts on index staleness | Pure n8n automation. Deterministic. Right level for what it does. |
| Safe DB Access | `L7 MAX GOAL-L7` | Enforces allowlists, blocks prohibited operations, logs all queries | Deterministic enforcement. No AI discretion needed or wanted. |

## Communication

| Workflow | Tag | What It Does | Gap to Target |
|----------|-----|--------------|---------------|
| Slack Integration | `L6 WIP GOAL-L8` | Receives commands, routes to appropriate workflows, sends acknowledgments | Needs: handle ambiguous commands without human clarification (→L7), self-heal on delivery failures (→L8) |
| Email Intelligence | `L7 WIP GOAL-L8` | Classifies inbound email, extracts invoice data, routes to expenses or review queue | Needs: self-heal when email provider API changes response format |

## Session Management

| Workflow | Tag | What It Does | Gap to Target |
|----------|-----|--------------|---------------|
| Session Orchestration | `L6 WIP GOAL-L8` | Manages context continuity across AI sessions, handles state handoffs | Needs: proactive checkpoint triggers (→L7), auto-recovery from mid-session failures (→L8) |

---

## Distribution Summary

| Tier | Levels | Count | Notes |
|------|--------|-------|-------|
| Manual | L1–L3 | 0 | All workflows are at minimum scheduled/triggered |
| Supervised | L4–L6 | 4 | Run reliably, human reviews output or enforces ceiling |
| Autonomous + Monitoring | L7–L9 | 10 | Run independently, alert on issues, most self-heal |
| Full Autonomy | L10 | 0 | By design — no single workflow needs self-improvement |

**Vacation-ready (L8+):** 3 workflows at target. 7 on upgrade path.

---

## Critical Path

The upgrade priority isn't "highest level possible." It's position on the critical path:

```
Product Research → Content Generator → Content Publisher → Site Live → Revenue
```

A stalled L5 on the critical path blocks revenue. An L4 off the critical path is fine at L4. That's what determined which WIP workflows got upgraded first.
