# Candidate Families — Strategic Thesis
*Written: 2026-04-07 | Agent: Hermes | Status: Hypothesis — needs validation*

---

## What the Data Shows So Far

189 Blueprint-compatible candidates at risk_approved as of 2026-04-07.
These are mostly POW Banker candidates that now pass BLUEPRINT_AGGRESSIVE gates.
Fresh Blueprint EA backtests (structural pairs) still running — results pending.

### By Symbol (risk_approved)

| Symbol | Count | Max PF | Median PF | Notes |
|--------|-------|--------|-----------|-------|
| GBPUSD | 75 | 31.3 | 10.2 | Most tested, noisy distribution |
| EURJPY | 63 | 53.4 | 11.9 | Best top-end, high variance |
| USDCAD | 19 | 43.5 | 10.4 | Proven live (Magic 777) |
| GBPJPY | 17 | 42.4 | 24.6 | HIGH median — cleanest signal |
| EURUSD | 7 | 14.9 | 11.8 | Consistent but modest |
| USDJPY | 4 | 8.4 | 6.9 | Weak — probably not suitable |
| NZDUSD | 2 | 48.0 | 48.0 | Only 2 but one is exceptional |
| USDCHF | 2 | 6.8 | 6.8 | Weak |

**Immediate observation:** GBPJPY has the highest median PF (24.6) of any
symbol with meaningful sample size. This is not noise — 17 candidates all
performing well suggests a structural edge, not a lucky parameter hit.

---

## The Three Buckets (Initial Hypothesis)

### Bucket 1 — HIGH CONVICTION WORKHORSES
*Deploy always. Funded accounts. Low drama.*

**Criteria:** Consistent median PF across symbol (not just top outliers),
low DD, long backtest periods, high trade count (15+ sequences).

**Current best candidates:**
- USDCAD: proven live as Magic 777. Median PF 10.4, DD ~4.4%
- GBPJPY: highest median, 17 candidates all strong. DD ~4.2%
- NZDUSD #11097: PF=48 is extraordinary. Needs verification.

**Why GBPJPY is surprising here:** It's a session harvester (high vol cross)
but the median PF of 24.6 suggests the grid recovers fast after spikes.
The Japan session creates the spike; London session creates the recovery.
If true across different parameter sets, this is structurally robust.

### Bucket 2 — HIGH PERFORMANCE OPPORTUNISTS
*Deploy on challenges. Higher risk, higher reward.*

**Criteria:** Top-end PF (>30), willing to accept more DD, shorter backtest
periods OK because we're using for prop firm challenges not long-term funded.

**Current best candidates:**
- EURJPY #19285: PF=53.4, 55 trades over 3 years — best sample size
- USDCAD #3586: PF=43.5 — but only 14 trades (thin sample, watch it)
- GBPJPY #3380: PF=42.4, 30 trades — solid
- NZDUSD #11097: PF=48, 17 trades — intriguing if confirmed

**Risk:** These are selected at peak PF. Monte Carlo pass probability matters
here. A PF=53 with MC=0.60 is less reliable than PF=25 with MC=0.95.
Need MC data before promoting these to challenge stacks.

### Bucket 3 — REGIME-SPECIFIC SPECIALISTS
*Deploy only when regime conditions confirmed. The "wardrobe" concept.*

**Not yet built.** These need:
1. Live regime detection (Hurst + ADX rolling calculation)
2. Parameter sets specifically tuned for RANGE_HIGH_VOL vs RANGE_LOW_VOL
3. Activation/deactivation logic in the copier

**Target symbols when ranging confirmed:**
- EURUSD: 7 candidates all PF 8-15 range, consistent. Deploy when H<0.47
- GBPUSD: 75 candidates, wide variance. Only use top 3-5 during ranging
- AUDNZD, EURGBP, EURCHF: structural rangesters — results pending

---

## The 3-Per-Symbol FT Selection Framework

You asked for 3 per symbol that "behave differently." Here's how to think
about selecting them:

### What "behave differently" means for a grid EA:

Each candidate has a different parameter fingerprint. The key axes of
differentiation are:

1. **DelayTradeSequence** — when in the day it enters
   - Low (1-3): enters early in session, catches full move
   - High (7-9): waits for session to develop, misses false starts

2. **LockProfit / TrailingStoploss ratio** — how it exits
   - High LP, high Trail: waits for big moves, gives back more
   - Low LP, low Trail: snaps out quickly, smaller wins, more frequent

3. **MaxOrders / PipStep combination** — how deep it grids
   - Wide step + many orders: handles big trending moves
   - Tight step + few orders: efficient in tight ranges

### Ideal 3-pack per symbol:

For USDCAD you'd want something like:
- **Alpha:** Low delay (fast entry), moderate LP, tight grid — profits in volatile days
- **Beta:** High delay (patient entry), high LP, wide grid — profits in trending recovery
- **Gamma:** Medium everything — consistent baseline, different enough to add diversification

The simulator can then overlay their equity curves and check:
- Do their drawdown periods coincide? (bad — correlated risk)
- Does one make money when another is in DD? (good — natural hedge)
- Combined max DD of all 3 running simultaneously? (must stay under 4.8%)

---

## What We Need To Know Next

### For selecting the 3-per-symbol FT shortlist:

1. **Monte Carlo pass probability per candidate** — currently stored in DB,
   need to surface it in the selection logic

2. **Trade timing distribution** — when in the day do sequences close?
   Two EURJPY candidates that both close at London open will stack DD.
   One EURJPY on London open + one on Asia close = natural diversification.

3. **Parameter fingerprint extraction** — currently the backtest HTML
   doesn't store parameters (inputs_json is empty for POW Banker backtests).
   Blueprint EA backtests will have this once EquityLogger is added.
   For now: use magic number → look up set file if it exists.

4. **GBPJPY deep investigation** — median PF 24.6 across 17 candidates
   is too good to not investigate. What parameters are they sharing?
   Are they all the same magic (777) just different time periods?
   Or genuinely different configurations that all work?

5. **Correlation analysis across symbols** — before we build a stack,
   know which symbols move together in DD. GBPUSD and EURUSD will often
   DD simultaneously (USD news). GBPJPY and EURJPY will often DD together
   (JPY moves). Ideal stack has low correlation.

### For regime detection:

6. **Build regime windows for 2023-2026 per symbol** — identify which 
   months each symbol was ranging vs trending. Then check: do our
   candidates perform better in the ranging windows?

---

## Preliminary FT Shortlist (pending Monte Carlo + parameter verification)

These are the candidates worth deep investigation before FT promotion:

| # | Symbol | Candidate | PF | Trades | Why |
|---|--------|-----------|-----|--------|-----|
| 1 | EURJPY | #19285 | 53.4 | 55 | Best sample, 3yr window |
| 2 | USDCAD | #3586 | 43.5 | 14 | Proven symbol, need more trades |
| 3 | GBPJPY | #3380 | 42.4 | 30 | Good sample, strong median |
| 4 | NZDUSD | #11097 | 48.0 | 17 | Exceptional — verify not a fluke |
| 5 | EURJPY | #909 | 38.4 | 25 | Different period from #19285 |
| 6 | USDCAD | #5303 | 42.6 | 16 | Cluster check with #3586 |
| 7 | GBPJPY | #4125 | 41.0 | 14 | Same symbol as #3380, different params |
| 8 | EURJPY | #4936 | 35.8 | 22 | Third EURJPY for diversity |
| 9 | GBPUSD | #15475 | 31.3 | 23 | Best of 75 GBPUSD |

**Note:** Candidates 2 and 6 (both USDCAD top PF) and 1 and 5 (both EURJPY)
may have correlated drawdowns — before promoting as a pair, check their
equity curves for temporal correlation.

---

## What's Still Missing

**The structural mean-reverters (AUDNZD, EURGBP, EURCHF, CADCHF)** have
zero candidates in this list because they're only being tested now with
the new intelligent queue. First results expected today/tonight.

**Hypothesis:** These will produce lower PF (8-15 range) but more consistent,
lower DD candidates. They belong in Bucket 1 (workhorses) not Bucket 2
(opportunists). If this holds, we'll have a clean separation:

- **Bucket 1 (funded, consistent):** AUDNZD, EURGBP, EURCHF, USDCAD
- **Bucket 2 (challenge, aggressive):** EURJPY, GBPJPY, NZDUSD
- **Bucket 3 (regime, opportunist):** EURUSD, GBPUSD when ranging confirmed

This is the EA wardrobe. Build it out over the next 2 weeks.
