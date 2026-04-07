# Discovery: Why Standard Gates Fail Grid EAs
*Discovered: 2026-04-07 | Agent: Hermes*

## The Core Mismatch

Standard pipeline gates were calibrated for **signal EAs** (NightRevert, DayBreak, SMC):
- Trade 3-8 times per day
- Each trade is independent
- 50 trades = ~2 weeks of data
- Max consecutive losses of 4 is meaningful

Grid basket EAs (POW Banker, Blueprint EA) are fundamentally different:
- Trade 1-3 times per MONTH (each "trade" = full sequence close)
- Trades are NOT independent (each is a multi-day/week position)
- 50 trades = 18-36 months of data (often exceeds backtest window)
- Consecutive loss streaks of 8+ are normal during ranging → trending transitions

## The Counting Problem

MT5 Strategy Tester reports "Total Trades" as basket closes (round-trips).
Each basket close represents:
- 3-8 grid levels opened progressively over days/weeks
- All closed simultaneously when LockProfit threshold hit
- One entry in the "Total Trades" count

Live trading records each individual position as a deal in the history.
So 14 "trades" in backtest = potentially 70-112 individual position deals.

**This is not a data quality issue — it's a semantic mismatch between how
grid EAs execute and how standard gates count.**

## The Kill Switch Correction

Standard compliance simulation assumes no external circuit breaker.
Our kill switch fires at 4.8% daily DD, converting any grid blowup into:
- A fixed bounded loss (~$4,800 on $100k)
- An automatic position close
- A reset to normal trading the next day

This changes the risk math fundamentally:
- A grid EA that "blows up" every 50 trades but earns $500/trade nets positive
- Standard sim would reject this; kill-switch-aware sim would approve it

## BLUEPRINT_AGGRESSIVE Gate Config

```json
min_trades: 15 (absolute), 0.5/month (duration-adjusted)
max_consecutive_losses: 8 pass / 10 rework / 11 reject  
min_profit_factor: 2.0 (stricter than standard 1.2)
monte_carlo: score_only, 0.60 threshold (non-binding)
time_slice: 3 slices, 2 of 3 valid, max_dispersion=2.0
```

The higher PF requirement (2.0 vs 1.2) compensates for the relaxed
trade count and consecutive loss thresholds. A grid EA must demonstrate
a stronger edge signal to pass with fewer trades.

## Future Work

- Model kill switch in Monte Carlo iterations (early termination at 4.8% DD)
- Calculate "net expected value" accounting for kill frequency × kill cost
- Build kill-switch-aware compliance simulation
