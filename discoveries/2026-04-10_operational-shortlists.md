# Operational Shortlists — Immediate Investigation vs Queue vs L2 vs FT
*Created: 2026-04-10 | Agent: Hermes*

## Purpose
Translate the mined families into an action-oriented shortlist for the next few hours of autonomous work.

## Lane A — Challenge-Fast

### Investigate Immediately
These candidates/families should be mined first for param extraction and family-causal comparison against the 777 family.

1. C3112 GBPUSD | POW_Banker_EA
- PF=148.55 | DD=8.79% | trades=7
- Old-gate mismatch candidate, prime hidden-gold challenge-fast example

2. C2395 GBPJPY | POW_Banker_EA
- PF=137.10 | DD=7.46% | trades=3
- Tiny sample but too extreme to ignore

3. C14533 GBPUSD | POW_Banker_EA
- PF=117.73 | DD=7.67% | trades=15
- Better sample than the ultra-low-trade outliers

4. C1270 EURUSD | POW_Banker_EA
- PF=113.76 | DD=6.53% | trades=6
- Suggests a possible aggressive EURUSD cousin family

5. C5110 GBPJPY | POW_Banker_EA
- PF=114.87 | DD=9.60% | trades=10
- Reinforces GBPJPY aggressive family thesis

### Queue Now
Queue targeted neighbourhood tests only after extracting shared params from the shortlist above.
Target shapes to test:
- LP/PS around 2.0
- DTS in {3,5}
- TS in {3,5,7}
- symbols: GBPUSD, GBPJPY, selective EURUSD

### Collect L2 / Sim First
Before challenge-stack decisions, collect or locate L2 for any shortlist candidate that survives family review.
Particularly important for:
- GBPUSD aggressive family
- GBPJPY aggressive family
- any candidate considered for challenge-fast deployment

### FT Candidate (conditional)
Only after family check + kill-switch-aware review:
- top surviving GBPUSD aggressive candidate
- top surviving GBPJPY aggressive candidate

## Lane B — Funded-Safe

### Investigate Immediately
1. C19793 AUDNZD | POW_Banker_EA
- PF=49.77 | DD=0.34% | trades=12

2. C19792 AUDNZD | POW_Banker_EA
- PF=40.09 | DD=0.21% | trades=11

3. C21802 AUDCAD | POW_Banker_EA
- PF=15.64 | DD=1.05% | trades=17

4. C19713 AUDNZD | POW_Banker_EA
- PF=4.78 | DD=1.11% | trades=176
- Lower PF but much stronger sample depth

5. C19721 AUDNZD | POW_Banker_EA
- PF=5.00 | DD=1.11% | trades=152

### Queue Now
- continue AUDNZD / AUDCAD neighbourhood exploitation
- continue CADCHF family exploitation
- tighten EURCHF translation rather than broad-copying CADCHF params

### Collect L2 / Sim First
Use L2 and challenge/funded sims for:
- AUDNZD funded-safe candidates
- AUDCAD funded-safe candidates
- CADCHF family additions where stack fit matters

### FT Candidate (conditional)
- best AUDNZD structural candidate if parameter family looks stable after review
- best AUDCAD structural candidate if family reinforcement holds

## Already Live / Monitor Closely
- C26295 GBPUSD | challenge-fast experimental FT
- C26282 CADCHF | funded-safe structural FT probe

## Rule
Do not deploy from shortlist directly.
Shortlist -> extract params -> family check -> L2/sim if needed -> decision.
