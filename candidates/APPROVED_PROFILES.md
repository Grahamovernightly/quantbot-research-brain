# Approved Candidate Profiles — Do Not Lose These
*Updated: 2026-04-07 | Maintained by: Hermes*

> These candidates have demonstrated exceptional metrics in backtesting.
> Some were suppressed by miscalibrated gates. All warrant live testing.

---

## Tier 1 — Extraordinary (PF > 30)

### #3586 — USDCAD | PF=43.47 | 14 trades
- **EA:** POW_Banker_EA (precursor to Blueprint)
- **Gate status:** REWORK (14 trades < 15 threshold — marginal miss)
- **Re-evaluate with:** ea_profile_id=10 (BLUEPRINT_AGGRESSIVE)
- **Why it matters:** USDCAD is a proven symbol (BB candidate already in FT). PF=43 is not noise over 14 sequences.
- **Action:** Re-evaluate and promote if passes

### #4125 — GBPJPY | PF=41.03 | 14 trades
- **EA:** POW_Banker_EA
- **Gate status:** REWORK (14 trades)
- **Family:** SESSION_HARVESTER (high vol, London session)
- **Why it matters:** GBPJPY at PF=41 with only 14 sequences suggests very clean mean-reversion entries
- **Action:** Re-evaluate and promote if passes

---

## Tier 2 — Excellent (PF 20-30)

### #5863 — GBPJPY | PF=33.81 | 13 trades
### #4139 — GBPJPY | PF=32.93 | 13 trades
### #2396 — GBPJPY | PF=32.93 | 13 trades
- Multiple GBPJPY candidates at similar PF — suggests a stable parameter cluster
- Worth finding the common parameters and exploiting the neighbourhood

### #20259 — USDCAD | PF=29.6 | 10 trades
- Fewer trades but extraordinary PF
- Duration-adjusted path should pass at 0.5/month threshold

### #1767 — EURUSD | PF=28.5 | 12 trades
### #8763 — EURUSD | PF=25.0 | 11 trades
- EURUSD at these PF levels is significant — typically harder symbol for grids

### #8150 — GBPUSD | PF=23.85 | 14 trades
### #3666, #1412 — EURJPY | PF=14.09 | 14 trades
### #176 — EURJPY | PF=13.48 | 14 trades

---

## Currently in Forward Test (pre-existing)

| ID | Symbol | PF | State |
|----|--------|----|-------|
| #6582 | USDCAD | 21.5 | forward_test |
| #11469 | EURJPY | 53.91 | forward_test |
| #16862 | EURJPY | 53.76 | forward_test |
| #3004 | EURUSD | 32.73 | forward_test |
| #9446 | EURJPY | 14.77 | forward_test |
| #11005 | USDCAD | 4.57 | forward_test |
| #2679 | EURJPY | 6.32 | forward_test |
| #11011 | EURJPY | 6.3 | forward_test |
| #596 | USDCAD | 8.33 | forward_test |
| #598 | USDCAD | 4.63 | forward_test |

EURJPY PF=53.91 and PF=53.76 are exceptional. Priority to understand their parameters.

---

## Parameter Extraction TODO
For each Tier 1/2 candidate: extract PipStep, LockProfit, TrailingStoploss, 
DelayTradeSequence, MaxOrders from their backtest set files.
These become the seed for neighbourhood exploitation in Phase 3.
