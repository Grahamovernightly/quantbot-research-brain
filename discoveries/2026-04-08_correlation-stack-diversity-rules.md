# Correlation & Stack Diversity Rules
*Date: 2026-04-08 | Source: Simulator agent review*

---

## Core Rule: One candidate per symbol per strategy

Adding near-identical candidates on the same symbol doubles concentration risk
for negligible marginal income. Worse — they will expand their grids simultaneously
on bad days, stacking DD that can blow the kill switch.

## Case Study: C3586 vs C5303 (both USDCAD Blueprint)

| Metric | C5303 ×0.5 | C3586 ×0.5 |
|--------|-----------|-----------|
| $/day | $42 | $41 |
| Worst DD | 3.29% | 3.31% |
| PipStep | 24 | 24 |
| DTS | 7 | 7 |
| LockProfit | 20 | 25 |
| TrailingStoploss | 1 | 7 |

- 24.4% of days both have >0.5% DD simultaneously
- Combined DD exceeds 3% on 11 days, 5% on 3 days
- Add BB USDCAD (7771): 3 USDCAD grids all expanding together on bad USDCAD days

**Decision: Use C3586 only.** TS=7 more protective than TS=1. 16 max positions vs 18.

## Stack Diversity Requirements

For a valid challenge stack addition, a new candidate must provide:
1. **Different symbol** — or structurally uncorrelated strategy on same symbol
2. **Different session** — Asian vs London vs NY reduces simultaneous DD days
3. **Different EA logic** — grid vs scalper vs breakout (NightRevert uncorrelated with POW Banker)
4. **Marginal income must justify correlation risk** — <$50/day addition not worth it

## CADCHF Sweep Implication

Even if we find 20 CADCHF candidates at PS=22/LP=35, we want AT MOST 1-2.
Pick the one with:
- Lowest worst intraday DD
- Longest data history (most reliable)
- Best PF
- NOT correlated with any other structural pair already in stack

EURCHF and AUDNZD are structural cousins to CADCHF — all three will correlate
during CHF risk events. Be careful stacking all three.

## Research Target: Symbol diversity map

Need winners on symbols NOT already in confirmed stack:
- Already covered: EURJPY, CADCHF, AUDNZD, AUDCAD, EURCHF, GBPCAD, USDCAD (×1 max more)
- Gaps to fill: GBPJPY (session harvester), NZDUSD (structural), GBPUSD (liquid)
- Blueprint strength: USDCAD proven — explore GBPUSD, GBPJPY with similar params
