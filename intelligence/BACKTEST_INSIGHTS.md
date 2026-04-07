# Backtest Intelligence Log
*Maintained by: Hermes | Updated after each significant batch*

---

## 2026-04-07 — First Blueprint Batch

### Volume
- ~400+ OHLC backtests completed across workers W03-W08
- 31 reports uploaded to MT5Suite before this entry
- Queue: rebalanced from random (PipStep 8-80) to regime-aware (8-30)

### Symbol Results
| Symbol | Backtests | Median PF | Max PF | Note |
|--------|-----------|-----------|--------|------|
| GBPUSD | 31 | 0.79 | 1.66 | First batch, mostly lottery params |
| EURJPY | ~50 | TBD | TBD | Running |
| AUDNZD | ~10 | TBD | TBD | Running — structural pair, expect better |
| EURGBP | ~10 | TBD | TBD | Running |

### Key Learning
GBPUSD median PF=0.79 with random params confirms: symbol selection and
regime-aware params matter enormously. The lottery produces losers.
Regime-intelligent items now in queue — expect improvement in next batch.

### Parameter Observations
- PipStep > 30 on majors: consistently bad (too wide, sequences don't close)
- PipStep 12-18 on GBPUSD: better signal/noise ratio
- LockProfit < $15: too tight, sequences close before meaningful profit
- LockProfit $20-35: sweet spot based on limited data so far

### Gate Performance
- Standard gates: 0 Blueprint passes so far (min_trades too high)
- BLUEPRINT_AGGRESSIVE: 20 candidates re-evaluated, all REWORK (min_per_month)
- After min_per_month fix (0.5): re-evaluation pending — expect multiple passes

---
*Next entry: after overnight batch completes (~08:00 UTC)*
