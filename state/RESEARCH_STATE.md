# Research State — Live Document
*Last updated: 2026-04-07 10:00 UTC | Updated by: Hermes (autonomous cron)*

---

## Current Phase
**Phase 2 — Signal from noise**

## Infrastructure Status
| Component | Status |
|-----------|--------|
| Workers W03-W08 | RUNNING |
| Research dispatcher | ACTIVE — 1min cron |
| Planner | ACTIVE — 20min cron |
| Regime intelligence | ACTIVE — 6hr cron |
| BLUEPRINT_AGGRESSIVE gates | LIVE — profile id=10 |
| Brain auto-update | ACTIVE — 1hr cron |

## Pipeline State (as of 2026-04-07 10:00 UTC)
| State | Count |
|-------|-------|
| forward_test | 7 |
| ingested | 1 |
| rejected | 3 |
| risk_approved | 189 |

**Queue depth:** 200 items

## Suppressed High-PF Candidates (re-evaluating under BLUEPRINT_AGGRESSIVE)
Candidates with PF>=2.0 but rejected under standard gates are being
automatically re-evaluated each hour under ea_profile_id=10.

## Active Hypotheses
1. Structural mean-reverters (AUDNZD/EURGBP/EURCHF) will have higher gate pass rate
2. PipStepExponent=1.3+ prevents cascade fills in session harvesters
3. SequenceCooldown=300 improves Monte Carlo pass rate
4. LotSizeExponent=1.0 improves compliance gate pass rate

*Next Telegram report: 08:00 UTC*
