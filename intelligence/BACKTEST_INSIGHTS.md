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

## 2026-04-09 — Live Near-Miss Review (Kamatera SSH + MT5Suite)

### What was checked
- Live dispatcher logs on Hetzner/Kamatera research factory
- MT5Suite candidate + backtest records for today's completed Blueprint_EA runs
- Live EquityLogger L2 CSVs pulled from Kamatera FILE_COMMON for review candidates

### Infra
- Workers W03-W07 active
- W08 appears stale/offline since 2026-04-07
- Queue depth still at 200 Blueprint work items

### Today's best completed candidates
| Candidate | Symbol | PF | Equity DD (HTML) | L2 worst day DD | $/day (L2) | Verdict |
|-----------|--------|----|------------------|-----------------|------------|---------|
| C26295 | GBPUSD | 1.97 | 31.88% | 10.88% | $174/day | Near-miss only — FT candidate, not challenge-core |
| C26287 | CADCHF | 1.71 | 8.41% | 4.79% | $65.8/day | Promising clean family member |
| C26282 | CADCHF | 1.69 | 6.67% | 4.71% | $63.1/day | Preferred CADCHF near-miss (lower DD) |
| C26291 | CADCHF | 1.67 | 8.30% | 4.49% | $57.5/day | Interesting but inferior to C26282 |
| C26241 | USDCAD | 1.62 | 7.53% | n/a | n/a | Weaker than prior USDCAD monsters |

### Key conclusions
- Do NOT lower the global PF>=2.0 gate. Today's live batch contains many sub-2.0 rejects that would create review spam if auto-promoted.
- Instead add a manual review band for PF 1.90-1.99 with strong MC + strong L2 profile.
- C26295 GBPUSD belongs in that near-miss review band immediately.
- C26282 CADCHF is the best live CADCHF promotion candidate because the DD is cleaner than C26287/26291.
- Existing Blueprint USDCAD winners (C3586/C5303) are still superior challenge-stack candidates to today's live batch.

### Challenge-stack impact (live sim refresh)
- Baseline confirmed 7-candidate stack still ~99.6% combined pass
- Adding C26295 GBPUSD at tiny sizing (x0.10-x0.12) is acceptable but satellite-only
- Adding C26282 CADCHF at x0.50 keeps stack stats strong and is more challenge-friendly than GBPUSD
- Replacing proven USDCAD slots with these new near-misses is NOT preferred

### Immediate operating recommendation
1. Keep C3586 as preferred Blueprint USDCAD challenge candidate
2. Prepare C26295 GBPUSD for experimental forward test on ForexVPS
3. Prepare C26282 CADCHF for forward test as the cleaner CADCHF family probe
4. Continue intelligent neighbourhood search around CADCHF rather than broad random sweeps

---
*Next entry: after further CADCHF/GBPUSD neighbourhood exploitation and FT verification*
