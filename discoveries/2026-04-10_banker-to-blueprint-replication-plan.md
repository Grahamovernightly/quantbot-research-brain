# Banker → Blueprint Replication Plan
*Created: 2026-04-10 | Agent: Hermes*

## Goal
Take the exact settings of strong Banker candidates and test whether Blueprint can achieve the same or better behavior using the same core settings.

This reduces long-term dependence on Banker and turns discovered Banker gold into Blueprint-native intelligence.

## Why this matters
- Banker already contains proven edge families
- Blueprint is the more extensible evolution
- If Blueprint can reproduce or improve strong Banker families, future research compounds on the better engine

## Replication doctrine
For each strong Banker candidate/family:
1. Extract exact Banker settings
2. Map those settings 1:1 into Blueprint where possible
3. Run a direct Blueprint backtest on the same symbol/date span
4. Compare:
   - PF
   - DD
   - trade count / sequence behavior
   - live suitability (challenge-fast vs funded-safe vs stack-booster)
5. If Blueprint underperforms, adjust only the Blueprint-native parameters that should improve it, not randomize broadly

## Initial replication targets

### Challenge-fast replication targets
1. Magic 777 family
- symbols: USDCAD, GBPUSD, EURUSD
- known shape: PS=15, LP=30, TS=5, DTS=3, ATR=1000, MaxOrders=20
- objective: see whether Blueprint can equal or beat the challenge-fast family on these symbols

2. Rejected aggressive GBPUSD family
- starting candidates: C3112, C14533 and neighbouring shortlist names
- objective: identify whether Blueprint can inherit the same family dynamics with better controls

3. Rejected aggressive GBPJPY family
- starting candidates: C2395, C5110
- objective: challenge-fast Blueprint translation with explicit caution on DD

### Funded-safe replication targets
1. CADCHF structural family
- current live Blueprint family already promising
- objective: compare against strongest Banker structural cousins

2. AUDNZD structural family
- starting candidates: C19793, C19792, C19713, C19721
- objective: see whether Blueprint can become a superior funded-safe expression

3. AUDCAD structural family
- starting candidate: C21802 and family neighbours
- objective: funded-safe Blueprint translation

## Replication workflow

### Step A — Extract source candidate params
Need exact Banker parameter set or nearest family representation.

### Step B — Build Blueprint-equivalent config
Use the same core values where fields exist in both systems.
Preserve especially:
- PipStep
- LockProfit
- TrailingStoploss
- DelayTradeSequence
- AtrPeriod
- MaxOrders
- LotSize / exponent behavior where meaningfully transferable

### Step C — Run direct A/B test
Same:
- symbol
- timeframe
- date range
Compare Banker vs Blueprint side by side.

### Step D — If Blueprint is close but worse
Only then use Blueprint-native controls to improve:
- SequenceCooldownSeconds
- MaxOrders tuning
- additional DD-governance controls
- any Blueprint-specific safety/structure improvements

## Classification rule after replication
Each replicated family should be assigned to one of three buckets:
1. challenge-fast
2. funded-safe
3. stack-booster

## Near-term implementation priority
1. Magic 777 family replication into Blueprint
2. AUDNZD funded-safe family replication into Blueprint
3. AUDCAD funded-safe family replication into Blueprint
4. GBPUSD/GBPJPY aggressive family replication into Blueprint

## Success condition
Success is not merely “Blueprint profitable.”
Success is:
- Blueprint matches or exceeds Banker family quality
- and produces a cleaner, more governable candidate family for future work
