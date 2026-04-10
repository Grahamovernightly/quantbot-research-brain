# Wave 2 — Family Extraction and Banker → Blueprint Replication Prioritization
*Created: 2026-04-10 | Agent: Hermes*

## Objective
Move beyond first-pass shortlist ranking and extract the actual family shapes worth porting into Blueprint.

## Challenge-Fast / Booster Family Extraction

### GBPUSD aggressive family
Key candidates:
- C14533 GBPUSD | PF=117.73 | DD=7.67%
- C3112 GBPUSD | PF=148.55 | DD=8.79%  → classify as stack-booster because frequency appears too low to be a true standalone challenge-fast leader

Extracted params:
- C14533: PS=25 LP=40 TS=1 DTS=9 ATR=500
- C3112: PS=45 LP=45 TS=6 DTS=9 ATR=500

Interpretation:
- This buried GBPUSD family is NOT a 777 clone.
- It is wider-step and much more selective than the 777 family.
- C14533 looks like a better challenge-fast replication target than C3112 because the parameter shape is less extreme.
- C3112 remains valuable as a stack-booster candidate.

### GBPJPY aggressive family
Key candidates:
- C2395 GBPJPY | PF=137.10 | DD=7.46%  → stack-booster / investigation target
- C5110 GBPJPY | PF=114.87 | DD=9.60%  → challenge-fast investigation target

Extracted params:
- C2395: PS=40 LP=50 TS=10 DTS=9 ATR=2000
- C5110: PS=35 LP=50 TS=10 DTS=7 ATR=1000

Interpretation:
- GBPJPY hidden-gold family is also NOT a 777 clone.
- It wants much wider PipStep, higher LockProfit, and a slower / more selective sequence delay.
- This supports the idea that the challenge-fast lane has multiple subfamilies, not one universal aggressive template.

### EURUSD aggressive family
Key candidate:
- C1270 EURUSD | PF=113.76 | DD=6.53%

Extracted params:
- C1270: PS=38 LP=40 TS=6 DTS=5 ATR=500

Interpretation:
- EURUSD hidden-gold family also sits in the wider-step, slower, selective camp.
- This may explain why the direct 777-style reading of EURUSD is weaker: a different aggressive family may fit EURUSD better.

## Funded-Safe Family Extraction

### AUDNZD structural family
Key candidates:
- C19793 AUDNZD | PF=49.77 | DD=0.34%
- C19792 AUDNZD | PF=40.09 | DD=0.21%
- C19713 AUDNZD | PF=4.78 | DD=1.11% | 176 trades
- C19721 AUDNZD | PF=5.00 | DD=1.11% | 152 trades

Extracted params:
- C19793: PS=25 LP=25 TS=1 DTS=3 ATR=1500
- C19792: PS=25 LP=20 TS=3 DTS=3 ATR=1000
- C19713: PS=15 LP=10 TS=5 DTS=3 ATR=500
- C19721: PS=15 LP=10 TS=9 DTS=3 ATR=500

Interpretation:
- AUDNZD appears to contain at least two structural subfamilies:
  1. PS=25 LP=20-25 DTS=3 family
  2. PS=15 LP=10 DTS=3 family
- The common constant is DTS=3 and very controlled DD.
- This is a major funded-safe mining lane.

### AUDCAD structural family
Key candidate:
- C21802 AUDCAD | PF=15.64 | DD=1.05%

Extracted params:
- C21802: PS=45 LP=5 TS=7 DTS=3 ATR=500

Interpretation:
- AUDCAD may be a structurally different low-DD family than AUDNZD.
- It looks extreme on PS/LP, so Blueprint replication is especially useful to see if the edge is portable or just a Banker artifact.

## Banker → Blueprint Replication Queue (created)
The following exact-setting Blueprint replications were queued:
- wi#68804 GBPUSD from C14533 params
- wi#68805 GBPJPY from C5110 params
- wi#68806 EURUSD from C1270 params
- wi#68807 AUDNZD from C19793 params
- wi#68808 AUDNZD from C19792 params
- wi#68809 AUDNZD from C19713 params
- wi#68810 AUDCAD from C21802 params

Current status at creation check:
- 68804 leased
- 68805 leased
- 68806 leased
- 68807 leased
- 68808 leased
- 68809 queued
- 68810 queued

## Priority conclusions

### Highest-value challenge-fast replication targets
1. C14533 GBPUSD → Blueprint
2. C5110 GBPJPY → Blueprint
3. C1270 EURUSD → Blueprint

### Highest-value stack-booster investigation targets
1. C3112 GBPUSD
2. C2395 GBPJPY

### Highest-value funded-safe replication targets
1. C19793 AUDNZD → Blueprint
2. C19792 AUDNZD → Blueprint
3. C19713 AUDNZD → Blueprint
4. C21802 AUDCAD → Blueprint

## Main finding
The rejected pool contains more than one hidden-gold family shape.
At minimum we now have evidence for:
- 777-style challenge-fast family
- wider-step selective aggressive GBPUSD/GBPJPY/EURUSD family
- structural AUDNZD funded-safe family
- structural AUDCAD funded-safe family
