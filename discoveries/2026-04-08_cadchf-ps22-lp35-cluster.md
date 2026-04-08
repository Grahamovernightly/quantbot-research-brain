# CADCHF Blueprint Parameter Cluster Discovery
*Date: 2026-04-08 | Agent: Hermes*

## Finding

After 650+ Blueprint backtests, a clear winning cluster emerged on CADCHF:

**PipStep=22, LockProfit=35 is the anchor**

All 7 CADCHF results with PF>=1.5 share EXACTLY PS=22 and LP=35:

| bt_id | PF   | PS | LP | DTS | TS | ATR  |
|-------|------|----|----|-----|----|------|
| 26070 | 1.71 | 22 | 35 | 5   | 6  | 1800 |
| 26645 | 1.70 | 22 | 35 | 1   | 4  | 1000 |
| 26072 | 1.68 | 22 | 35 | 5   | 10 | 1800 |
| 26753 | 1.68 | 22 | 35 | 3   | 4  | 1500 |
| 25992 | 1.66 | 22 | 35 | 9   | 10 | 500  |
| 26647 | 1.60 | 22 | 35 | ?   | 4  | ?    |
| 26646 | 1.52 | 22 | 35 | ?   | ?  | ?    |

DTS ranges 1-9, ATR 500-1800 — all pass with PF 1.5-1.71.
TS seems to not matter (1-11 all appear).

## Interpretation

CADCHF is a STRUCTURAL mean-reversion pair (H≈0.44).
PipStep=22 aligns with its daily ATR — tight enough to catch mean-reversion
but wide enough to avoid cascade fills.
LockProfit=35 ($35 target) works across all time periods.

## Action Taken

200 targeted jobs submitted exploiting the PS=22/LP=35 neighbourhood:
- PS range: 18-26
- LP range: 25-45
- All DTS/TS/ATR combinations
Goal: Find PF>=2.0 within this cluster to achieve gate pass.

## Next Steps

1. Watch for PF>=2.0 in this batch (expected within 2-4 hours at current throughput)
2. If PF>=2.0 found: submit to BLUEPRINT_AGGRESSIVE gate (ea_profile_id=10)
3. Cross-symbol test: try same PS=22 LP=35 on EURCHF and AUDNZD (structural cousins)
