# Rejected Pool Shortlists — Challenge Fast vs Funded Safe
*Created: 2026-04-10 | Agent: Hermes*

## Purpose
Create a first organized shortlist from the rejected candidate pool using the two-lane agenda:
1. challenge-fast
2. funded-safe

This is a triage artifact, not a final deployment list.

## Challenge-Fast Shortlist (first pass)
These candidates look promising because they were rejected mainly by old governance logic (especially min_trades) despite extreme PF.

### Tier 1 — immediate closer investigation
1. C3112 GBPUSD | POW_Banker_EA
- PF=148.55
- DD=8.79%
- trades=7
- rejection: min_trades
- Interpretation: exactly the kind of candidate the old gate stack would wrongly bin despite huge challenge-fast potential

2. C2395 GBPJPY | POW_Banker_EA
- PF=137.10
- DD=7.46%
- trades=3
- rejection: min_trades
- Interpretation: tiny sample, but absurd PF and manageable DD makes this worth immediate family-level investigation

3. C14533 GBPUSD | POW_Banker_EA
- PF=117.73
- DD=7.67%
- trades=15
- rejection: soft gate / rework path
- Interpretation: stronger sample than the ultra-low-trade outliers; excellent candidate for challenge-fast family review

4. C1270 EURUSD | POW_Banker_EA
- PF=113.76
- DD=6.53%
- trades=6
- rejection: min_trades
- Interpretation: important because it suggests the 777-style aggressive family may have hidden EURUSD variants worth revisiting carefully

5. C5110 GBPJPY | POW_Banker_EA
- PF=114.87
- DD=9.60%
- trades=10
- rejection: min_trades
- Interpretation: GBPJPY challenge-fast family deserves dedicated mining, not one-off curiosity

### Tier 2 — family-cluster reinforcement
- C9524 GBPUSD PF=119.23 DD=9.67 trades=12
- C4396 GBPUSD PF=102.93 DD=9.67 trades=12
- C16230 GBPUSD PF=94.12 DD=8.51 trades=12
- C17653 GBPUSD PF=77.92 DD=4.90 trades=12

Interpretation:
- GBPUSD rejected aggressive family is clearly not random noise
- multiple high-PF low-trade candidates cluster in the same symbol/family
- this is exactly the type of pocket to mine for challenge-fast lane

## Funded-Safe Shortlist (first pass)
These candidates look promising because they combine low DD and structurally calmer symbols/families.

### Tier 1 — structural family leaders
1. C19793 AUDNZD | POW_Banker_EA
- PF=49.77
- DD=0.34%
- trades=12
- rejection: min_trades
- Interpretation: extraordinary funded-safe signal; very high priority for deeper investigation

2. C19792 AUDNZD | POW_Banker_EA
- PF=40.09
- DD=0.21%
- trades=11
- rejection: min_trades
- Interpretation: reinforces AUDNZD as a major funded-safe family candidate

3. C21802 AUDCAD | POW_Banker_EA
- PF=15.64
- DD=1.05%
- trades=17
- rejection: min_trades
- Interpretation: strong funded-safe structural signal

4. C19713 AUDNZD | POW_Banker_EA
- PF=4.78
- DD=1.11%
- trades=176
- rejection: compliance / target not reached
- Interpretation: lower PF than the top outliers but much larger sample and still very controlled DD; strong autopilot-style candidate

5. C19721 AUDNZD | POW_Banker_EA
- PF=5.00
- DD=1.11%
- trades=152
- rejection: compliance / target not reached
- Interpretation: confirms the family is robust beyond tiny-sample outliers

### CADCHF note
CADCHF remains the strongest live structural refinement lane in Blueprint, but this first rejected-pool shortlist suggests AUDNZD and AUDCAD may be even more attractive funded-safe mining lanes inside the legacy Banker pool.

## Implications

### Challenge-fast lane
Focus next on:
- rejected GBPUSD aggressive family
- rejected GBPJPY aggressive family
- rejected EURUSD aggressive family
- compare them causally against the live 777 family shape

### Funded-safe lane
Focus next on:
- rejected AUDNZD structural family
- rejected AUDCAD structural family
- continue CADCHF Blueprint family translation and comparison

## Immediate next mining actions
1. Extract params for Tier 1 challenge-fast shortlist and compare against 777-family shape
2. Extract params for Tier 1 funded-safe shortlist and compare against CADCHF/AUDNZD/AUDCAD structural hypotheses
3. Where L2 exists, run challenge-stack or funded-fit analysis instead of relying only on L1 metrics
