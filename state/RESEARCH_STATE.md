# Research State — Live Document
*Last updated: 2026-04-07 02:01 UTC | Updated by: Hermes (autonomous cron)*

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

## Pipeline State (as of 2026-04-07 02:01 UTC)
| State | Count |
|-------|-------|
| forward_test | 7 |
| gate_passed | 172 |
| ingested | 1 |
| rejected | 19 |
| risk_approved | 1 |

**Queue depth:** 200 items

## 🚀 New Gate Passes This Cycle
- #3666 EURJPY PF=14.1 trades=14
- #1412 EURJPY PF=14.1 trades=14
- #176 EURJPY PF=13.5 trades=14
- #6909 EURJPY PF=10.3 trades=14
- #5449 EURJPY PF=10.6 trades=14
- #3586 USDCAD PF=43.5 trades=14
- #5863 GBPJPY PF=33.8 trades=13
- #4139 GBPJPY PF=32.9 trades=13
- #2396 GBPJPY PF=32.9 trades=13
- #8150 GBPUSD PF=23.9 trades=14
- #4125 GBPJPY PF=41.0 trades=14
- #5891 GBPJPY PF=9.9 trades=13
- #2352 GBPJPY PF=10.1 trades=13
- #1284 EURUSD PF=8.4 trades=14
- #4278 EURUSD PF=12.7 trades=14
- #2544 EURUSD PF=8.8 trades=14

## Suppressed High-PF Candidates (re-evaluating under BLUEPRINT_AGGRESSIVE)
Candidates with PF>=2.0 but rejected under standard gates are being
automatically re-evaluated each hour under ea_profile_id=10.

## Active Hypotheses
1. Structural mean-reverters (AUDNZD/EURGBP/EURCHF) will have higher gate pass rate
2. PipStepExponent=1.3+ prevents cascade fills in session harvesters
3. SequenceCooldown=300 improves Monte Carlo pass rate
4. LotSizeExponent=1.0 improves compliance gate pass rate

*Next Telegram report: 08:00 UTC*
