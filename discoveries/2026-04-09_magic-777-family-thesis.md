# Magic 777 Family Thesis
*Created: 2026-04-09 | Agent: Hermes*

## Summary

Magic 777 is not special because of the number itself.
It is special because a specific aggressive POW Banker configuration family is extremely well matched to certain symbols and to a kill-switch-protected challenge-passing context.

## Known live family members
- 777 master
- 7771 USDCAD copier/live child
- 7772 EURUSD child
- 7773 GBPUSD child

## Extracted parameter shape
From extracted 7772/7773 set files:
- PipStep = 15
- LockProfit = 30
- TrailingStoploss = 5
- DelayTradeSequence = 3
- AtrPeriod = 1000
- PipStepExponent = 1.2
- LotSize = 0.35
- LotSizeExponent = 1.2
- MaxOrders = 20
- No EMA / RSI / ADX gating
- No high-impact news filter
- Broad custom trading window

## Why this family likely works

### 1. LP/PS ratio = 2.0
This ratio keeps reappearing in winner analysis.
- large enough target to let baskets mean-revert meaningfully
- not so large that exits become too rare

### 2. DelayTradeSequence = 3
This appears to be a sweet spot:
- not immediate overtrading
- not too inert
- enough delay to avoid some bad second-order fills while keeping challenge pace high

### 3. Tight-but-not-too-tight PipStep = 15
On the right symbols, this harvests repeated small-to-medium mean reversions.
- especially good on USDCAD
- works on GBPUSD when regime is cooperative
- more fragile on EURUSD trend periods

### 4. MaxOrders = 20 + kill switch = aggressive challenge engine
Without external controls this is dangerous.
With copier kill switches, the tail is capped.
That changes the optimisation objective:
- maximise challenge speed
- tolerate bounded kill events
- do not optimise as if the grid can expand forever

## Symbol interpretation

### USDCAD
Best current expression of the family.
Why likely strong:
- structurally lower-volatility commodity-linked major
- enough oscillation for grid harvesting
- lower trend damage than many majors
- challenge-safe relative to its earning rate

### GBPUSD
Strong but riskier expression.
Why:
- larger swings create excellent earning velocity
- but deeper / messier excursions increase DD and challenge-stack toxicity
- better as challenge-fast satellite than funded-safe core

### EURUSD
Can work, but less robust.
Why:
- lower raw noise harvest than GBPUSD
- vulnerable to trend periods where the 15/30 shape becomes too blunt
- should not be treated as equally strong just because it shares the family

## Main conclusion

Magic 777 family belongs in the **challenge-fast lane**, not the funded-safe lane.

### Challenge-fast lane
Use when:
- objective is to pass a challenge quickly
- kill switches cap daily/max DD
- higher turnover and higher earnings velocity matter more than perfect smoothness

### Funded-safe lane
Do NOT treat 777 family as the ideal funded-autopilot family.
For funded-safe, structural families like CADCHF / AUDNZD / AUDCAD / EURCHF are more appropriate.

## Immediate research implication

We should mine the rejected pool for other candidates that match this causal pattern:
- aggressive Banker / Blueprint family
- LP/PS near 2.0
- modest DTS delay
- high PF but rejected for old gate reasons
- symbols with similar microstructure to USDCAD / selective GBPUSD

## What remains to be done

1. Extract 7771 parameters explicitly (not just 7772/7773)
2. Compare 777 family against nearby variants:
   - PS 13 / 15 / 17
   - LP 25 / 30 / 35
   - DTS 1 / 3 / 5 / 7
   - TS 3 / 5 / 7
3. Build a challenge-fast shortlist from rejected Banker / Blueprint candidates that resemble this family
