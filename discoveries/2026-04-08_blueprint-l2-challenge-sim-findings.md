# Blueprint EA L2 Challenge Simulator Findings
*Date: 2026-04-08 | Agent: Hermes*

---

## Summary

First proper L2 (100k deposit) equity curve data collected for Blueprint_EA candidates.
Challenge simulator run against confirmed 7-candidate stack.

## Key Finding: Only USDCAD is challenge-safe

At 100k deposit, Blueprint EA grid positions create 20-27% intraday equity DD on
volatile pairs (EURJPY, GBPJPY, NZDUSD). Even at ×0.5 multiplier on the challenge
account, this exceeds the 4.8% kill switch threshold constantly → unusable.

USDCAD is the exception: worst intraday DD ~6% at 100k, manageable.

## L2 Data Collected (100k base, EquityLogger format)

| Candidate | Symbol | PF    | Days | Worst DD | $/day | Challenge viable? |
|-----------|--------|-------|------|----------|-------|-------------------|
| #3586     | USDCAD | 43.47 | 299  | 6.25%    | +$73  | YES ×0.5          |
| #5303     | USDCAD | 42.64 | 299  | 6.11%    | +$73  | YES ×0.5          |
| #19285    | EURJPY | 53.38 | 300  | 19.80%   | -$268 | NO — grid blows   |
| #11097    | NZDUSD | 48.01 | 638  | 26.92%   | +$38  | NO — dd too high  |
| #2396     | GBPJPY | 32.93 | 120  | 18.95%   | -$640 | NO — net negative |
| #176      | EURJPY | 13.48 | 213  | 19.55%   | -$404 | NO — net negative |

## Challenge Simulator Results (FTMO 2-Step Swing 100k)

Baseline (confirmed 7-cand stack): 99.6% combined | 29d/14d | $4,613/mo

| Addition         | Combined% | P1 days | $/mo     | Notes              |
|------------------|-----------|---------|----------|--------------------|
| #3586 ×0.5       | 98.2%     | 26d     | +$1,536  | SAFE               |
| #5303 ×0.5       | 98.0%     | 26d     | +$1,536  | SAFE               |
| Both ×0.5 each   | ~97.5%    | 25d     | +$3,072  | Recommended add    |

## Root Cause: Why EURJPY/GBPJPY are challenge-incompatible

LotSize=0.35 per 100k with MaxOrders=15-22 on volatile pairs creates grid stacks
worth 5-8 lots floating at depth. On EURJPY a 100 pip adverse move at 5 lots = $5,000
floating loss = 5% of account = kill fires. This is by design in the grid EA — it
needs large accounts or must use lower LotSize for challenge context.

## Recommendation for Challenge Context

1. Use Blueprint USDCAD candidates (#3586, #5303) at ×0.5 multiplier
2. For EURJPY/volatile pairs: need Blueprint config with LotSize=0.10 (not 0.35)
   to bring intraday DD under 2% → would allow ×2+ multiplier on challenge
3. This is a separate "challenge-optimised" set file, not the funded account config

## Forward Test Decision

#3586 USDCAD PF=43.47 and #5303 USDCAD PF=42.64 promoted to forward_test.
Blueprint_EA ea_id=16, both risk_approved, promotable=True.
Set files: PipStep=24 (same for both), LockProfit=25/20 respectively.
