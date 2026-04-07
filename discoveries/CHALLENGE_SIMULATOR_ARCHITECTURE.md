# Challenge Simulator — Architecture Assessment & App Recommendation
*Written: 2026-04-07 | Agent: Hermes*

---

## Current State

The challenge simulator exists as:
1. **L1 simulator** — Supabase edge function proxy at `olcvhmhdwowoulzyipds.supabase.co/functions/v1/simulator-proxy`. Uses closed-trade PnL only. Good for screening.
2. **L2 simulator** — Python script written inline per session. Kill-switch-aware Monte Carlo. Uses daily equity bar data. Required for final decisions.
3. **L2 data store** — CSV files in `/Users/g/Documents/EA L2 data/`. Manually curated.

The system works but has critical gaps:
- L2 simulator has to be rewritten from scratch each session (no persistent code)
- L2 data collection is manual (no automatic pipeline from backtest → CSV)
- Stack design is ad-hoc (no canonical "current best stack per firm" record)
- Blueprint EA candidates have no L2 data at all yet (EquityLogger not built)
- No automatic re-simulation when new candidates are promoted to risk_approved

---

## Should We Build a Proper App?

**Short answer: Yes, but not yet. Build the data foundation first.**

The bottleneck is not the simulator — it's data. The simulator is fast (5,000 iterations in ~20s). What's slow is:
1. Getting L2 data for new candidates
2. Deciding which candidates to include in a stack
3. Running the sim correctly every time without bugs

A proper app solves (3) and makes (2) faster, but can't fix (1). Until every risk_approved candidate automatically produces an L2 CSV, the app would just simulate the same 15 candidates we already have.

**The right build sequence:**
1. EquityLogger in Blueprint EA → L2 data auto-generated from every backtest (Claude Code task — 2hrs)
2. Auto-extraction pipeline → when candidate hits risk_approved, L2 CSV extracted and saved (Hetzner cron)
3. Then build the app — by that point it has real data to work with

**What the app should be when we build it:**

Not a full web app. A FastAPI service on Hetzner with a clean API that:
- `GET /candidates` — list all candidates with L2 data availability
- `POST /simulate` — run L2 Monte Carlo against a stack + firm, return structured results
- `GET /stacks` — saved stack configurations per firm
- `POST /optimize` — given a firm and candidate pool, find optimal multipliers
- `GET /stacks/{firm}/recommendation` — current best stack for this firm

The frontend can be as simple as the Nerve Centre dashboard calling these endpoints. Or just Telegram commands. Or just me querying it directly.

**Estimated build time:** 1 day for the API, 1 day for auto-extraction pipeline.
**Prerequisite:** EquityLogger in Blueprint EA first.

---

## What I Need to Run Simulations Now (Hermes KB)

I now have full access to run simulations. Requirements:

**For any simulation request:**
1. L2 CSV files must exist locally in `/Users/g/Documents/EA L2 data/`
2. Must specify: firm, candidates, multipliers, kill threshold
3. Output: pass rate, blow rate, median days, kills/attempt, kill frequency

**Never:**
- Use cached results from previous sessions
- Guess multipliers without running the sim
- Use L1 data for final decisions
- Hardcode $100k base (auto-detect from CSV row 0)

**Verified baseline to cross-check against:**
- FTMO 2-step, 16-cand stack: 99.9% pass, 8d, 0.27 kills
- BB USDCAD solo ×1.0: ~100% pass, ~34d

---

## Blueprint EA → Simulator Integration Plan

**Current gap:** Blueprint candidates have no L2 data.

**What we have from MT5Suite equity endpoint:**
- Deal-by-deal equity snapshots (31 points for a 2-year backtest)
- No intraday low/high (suspect tier data)
- Can build approximate L2 but DD will be underestimated

**What we need:**
- EquityLogger in Blueprint EA writing `equity_MAGICNUMBER.csv` to Common Files
- Auto-extraction: after each backtest, if candidate passes gates, pull CSV
- Convert to standard L2 format and save to Blueprint candidates folder

**Until EquityLogger is built:**
- Can run L1-only simulations for Blueprint candidates via MT5Suite equity endpoint
- Flag all results as "L1 screening only — not final"
- Focus sim work on existing validated candidates (POW Banker, NightRevert, etc.)

---

## Stack Design Principles (distilled from skill + session learnings)

### The Two-Config Doctrine
Every firm gets TWO configs designed simultaneously:
- **PASS-FAST:** maximise speed, tolerate 1-5% blow rate, aggressive multipliers
- **FUNDED-SAFE:** near-zero kills, conservative multipliers (~50% reduction), remove dangerous candidates

The copier supports per-magic multipliers — switching is a config change.

### The Diversification Rule
A good stack has:
- 5-7 unique symbols (avoids USD-event correlation)
- Mix of grid (POW Banker/Blueprint) + signal (NightRevert/DayBreak/Pat_SD)
- Mix of sessions (Asian scalpers + London/NY grids)
- At most 2 candidates on same symbol ONLY if structurally uncorrelated (different EA logic)

### The Kill Switch as Strategy
Without kill switch: aggressive stacks blow 60-70%
With kill switch at 4.80%: same stacks pass 99%+

Key metrics per candidate:
- **Worst intraday DD %** (from L2 day_low_equity)
- **Kill frequency** (% of days where scaled DD ≥ 4.80%)
- **Kill-adjusted net earning** = normal_earning - (kill_freq × kill_cost)

If kill-adjusted net earning > 0 AND kill frequency < 5% → viable for stack

### Blueprint Candidate Placement (when L2 available)

Based on current analysis:
- **WORKHORSES (funded safe):** AUDNZD, EURGBP, EURCHF — structural mean-reverters, low DD
- **ACCELERATORS (challenge speed):** EURJPY PF=53, GBPJPY median PF=24 — high earning rate
- **DIVERSIFIERS (add for symbol coverage):** USDCAD, NZDUSD — proven, clean DD profile

Target stack architecture (Blueprint + existing):
- Keep existing 8-candidate core (validated at 99.2% P1+P2)
- Add 2-3 Blueprint candidates for speed boost
- Expected: 99.5%+ pass rate, 15-20 day median (down from 39 days with Blueprint accelerators)

---

## Questions to Answer Before Next Stack Design

1. Do any of the 189 risk_approved Blueprint candidates have Monte Carlo scores in the DB?
   If yes, filter for MC ≥ 0.70 before shortlisting for FT
   
2. What is the trade timing distribution for GBPJPY top candidates?
   If they all cluster at London open, they'll correlate with GBPUSD/EURUSD kills
   
3. Are the EURJPY top candidates from different time windows?
   #19285 (3yr window) vs #909 (6mo window) may look different in sim

4. What is the current FT slot capacity?
   If slots are full (noted: terminal full), need to clean up non-trading candidates first
   before promoting Blueprint candidates
