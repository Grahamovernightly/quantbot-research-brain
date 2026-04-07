# Discovery: Regime-Aware Parameter Selection
*Discovered: 2026-04-07 | Agent: Hermes*

## The Core Insight

A bidirectional grid EA's edge is not constant — it varies by:
1. **Mean reversion tendency** (Hurst exponent H < 0.5 = ranging)
2. **Volatility level** (ATR percentile vs own history)
3. **Trend strength** (ADX — above 25 = trending, kills grids)
4. **Session character** (when does volatility cluster?)

The same PipStep=15 that works on AUDNZD (structurally ranging, H≈0.41)
will fail on GBPUSD during a post-NFP trend (H≈0.58, ADX=35).

## Symbol DNA

Instruments have structural tendencies driven by economics:

### Structural Mean-Reverters (always use tight params)
- **AUDNZD** H≈0.41 — RBA/RBNZ always correlated, cannot trend long
- **EURGBP** H≈0.43 — post-Brexit equilibrium, institutionally range-bound  
- **EURCHF** H≈0.40 — SNB floor psychology, mean-reverts aggressively
- **CADCHF** H≈0.44 — commodity/safe-haven inverse oscillation
- **AUDCAD** H≈0.45 — two commodity currencies, correlated fundamentals

### Session Harvesters (use wide params, high vol)
- **EURJPY** H≈0.49 — London open spikes, Asia session oscillation
- **GBPJPY** H≈0.50 — widest daily range, violent but mean-reverting on 4h+
- **GBPCAD** H≈0.50 — London session driven, high vol range

### Opportunists (activate only when regime confirms ranging)
- EURUSD, GBPUSD, USDCAD, NZDUSD, USDJPY, USDCHF
- Check: Hurst < 0.48 AND ADX < 22 on D1 rolling 65 days

## Regime → Parameter Mapping

| Regime | PipStep | LockProfit | MaxOrders | LotSizeExp | PipStepExp |
|--------|---------|------------|-----------|------------|------------|
| RANGE_LOW_VOL | 8-16 | $10-25 | 10-15 | 1.0-1.1 | 1.0-1.1 |
| RANGE_NORMAL | 12-22 | $15-40 | 12-20 | 1.0-1.2 | 1.1-1.2 |
| RANGE_HIGH_VOL | 14-26 | $20-50 | 15-22 | 1.1-1.3 | 1.2-1.4 |
| TREND_LOW_VOL | 18-35 | $15-30 | 8-14 | 1.0 | 1.0-1.1 |
| TREND_HIGH_VOL | SKIP | SKIP | SKIP | SKIP | SKIP |

## Version Roadmap
- **v1 (live):** Structural priors — uses symbol DNA to set ranges
- **v2 (target week 2):** Rolling Hurst+ADX from live OHLC — detects regime shifts
- **v3 (target month 2):** Regime window backtesting — test only on dates when symbol was in right regime

## Code Location
`~/quantbot-scripts/blueprint-research/regime_intelligence.py` on Hetzner
