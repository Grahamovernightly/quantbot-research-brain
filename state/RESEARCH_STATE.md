# Research State — Live Document
*Last updated: 2026-04-07 02:55 UTC | Updated by: Hermes (autonomous)*

---

## Current Phase
**Phase 2 — Signal from noise**
Finding first gate-passing Blueprint configurations. Understanding which symbols and parameter families produce viable candidates.

## Infrastructure Status
| Component | Status |
|-----------|--------|
| Workers W03-W08 | RUNNING — 6 parallel OHLC backtests |
| Research dispatcher | ACTIVE — 1min cron per worker |
| Planner | ACTIVE — 20min cron |
| Regime intelligence v1 | ACTIVE — 6hr cron |
| BLUEPRINT_AGGRESSIVE gates | LIVE — profile id=10, Railway deployed |
| Telegram alerts | ACTIVE — gate pass + 08:00/20:00 UTC reports |

## Queue Status (last checked 02:50 UTC)
- Queued: 200+ items
- Symbol mix: EURJPY, AUDNZD, EURGBP, EURCHF, CADCHF, USDCAD, GBPUSD
- PipStep range: 8-30 (corrected from earlier 8-80 lottery)
- Regime metadata: present on intelligently-generated items

## Key Findings So Far

### The Magic 777 Discovery
POW Banker magic 777 (GBPUSD/EURUSD/USDCAD master) has:
- PF=10.70 live, WR=83%, RR=2.2:1
- $25,788 profit from 199 trades
- Max 8 consecutive losses
- Rejected by standard gates: only 14-27 trades in backtest window
- **Conclusion:** Standard gates are miscalibrated for basket-close grid EAs

### Candidates Being Suppressed (pending re-evaluation after gate fix)
These have extraordinary PF but just under min_trades threshold:
| Candidate | Symbol | PF | Trades | Gap |
|-----------|--------|----|--------|-----|
| #3586 | USDCAD | 43.47 | 14 | 1 trade short |
| #4125 | GBPJPY | 41.03 | 14 | 1 trade short |
| #5863 | GBPJPY | 33.81 | 13 | 2 trades short |
| #4139 | GBPJPY | 32.93 | 13 | 2 trades short |
| #8763 | EURUSD | 25.0 | 11 | 4 trades short |
| #1767 | EURUSD | 28.5 | 12 | 3 trades short |
| #8150 | GBPUSD | 23.85 | 14 | 1 trade short |
| #20259 | USDCAD | 29.6 | 10 | 5 trades short |

**Action:** min_per_month lowered to 0.5 and deployed. Re-evaluating these now.

### Gate Architecture
- Standard gates: min_trades=50, max_consec=4, min_pf=1.2
- BLUEPRINT_AGGRESSIVE (id=10): min_trades=15, max_consec=8, min_pf=2.0, min_per_month=0.5
- Standard gates kept intact — BLUEPRINT_AGGRESSIVE is additive only

## Active Hypotheses
1. **Structural mean-reverters will outperform on gate pass rate** (AUDNZD, EURGBP, EURCHF) — TESTING
2. **PipStepExponent=1.3+ prevents cascade fills in session harvesters** (EURJPY, GBPJPY) — TESTING
3. **SequenceCooldown=300 improves Monte Carlo pass rate** — QUEUED
4. **LotSizeExponent=1.0 improves compliance gate pass rate** — QUEUED

## Next Actions (autonomous, next 8 hours)
- [ ] Re-evaluate suppressed candidates under new gate (min_per_month=0.5)
- [ ] Monitor batch results and update intelligence log
- [ ] Run regime intelligence v2 planning pass
- [ ] Telegram 08:00 UTC morning report
- [ ] If any gate passes: promote to robustness, tag as AGGRESSIVE family
