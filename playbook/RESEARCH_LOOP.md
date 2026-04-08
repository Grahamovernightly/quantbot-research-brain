# Blueprint EA Research Loop
*Author: Hermes | Framework agreed with Graham 2026-04-08*

---

## The Loop: Find → Sharpen → Generalise → Enrich

### Phase 1: FIND
- Broad sweep across symbols and param space
- Goal: identify ANY cluster with PF >= 1.5 consistently
- Success signal: same symbol appearing multiple times with similar params
- Current find: **CADCHF PS=22 LP=35** (7/7 PF>=1.5 results)

### Phase 2: SHARPEN
- Tight grid around the winning cluster
- Goal: find the single BEST version — highest PF, lowest DD, most trades
- Vary only 1-2 params at a time around the anchor
- Selection criteria:
  1. Highest PF (primary)
  2. Lowest worst intraday DD (challenge sim viability)  
  3. Most trades (statistical confidence)
  4. Longest run without equity blowout
- Output: 1 champion candidate per symbol cluster (NOT multiple near-identical)

### Phase 3: GENERALISE
- Take the winning params from Phase 2
- Apply to structurally similar symbols:
  - CADCHF PS=22 LP=35 → try EURCHF PS=16-20 LP=28-35 (tighter pair, scale down)
  - CADCHF PS=22 LP=35 → try AUDNZD PS=14-18 LP=20-28 (even tighter)
  - USDCAD PS=24 LP=25 → try NZDUSD PS=20-26 LP=20-30 (commodity pair cousin)
- Also try session harvesters with scaled-up params:
  - GBPJPY PS=35-50 LP=35-50 (volatile, needs wider grid)
- Goal: build a diverse winner bank across uncorrelated symbols

### Phase 4: ENRICH (future)
- Once we have clean base winners per symbol, add filters:
  - Blueprint_SMA variant: only go long if price > SMA(200), only short if < SMA(200)
  - Blueprint_ADX variant: only trade if ADX < 25 (ranging filter)
  - Blueprint_RSI variant: entry bias from RSI(4) extreme readings
  - Blueprint_Session variant: restrict trading hours to best session for that symbol
- Test each filter: does it improve PF? Does it reduce DD? Does it kill trade frequency?
- A filter that adds 20% PF but halves trade frequency may not be worth it

## Correlation Rules (non-negotiable)
- ONE winner per symbol in the stack
- Structural pairs (CADCHF, EURCHF, AUDNZD, EURGBP) all correlate on CHF/commodity events — max 2 from this group
- USDCAD + BB USDCAD already in stack — no more USDCAD grid adds
- Session harvesters (GBPJPY, EURJPY) correlate on JPY events — max 1 JPY pair
- Liquid pairs (GBPUSD, EURUSD) correlate on USD risk days — max 1 at a time

## Current State (2026-04-08)
- Phase 1 complete: CADCHF PS=22/LP=35 cluster found
- Phase 2 active: 200 tight neighbourhood jobs submitted
- Phase 3 queued: will start once Phase 2 champion identified
- Phase 4: not started — needs 3+ validated Phase 3 winners first
