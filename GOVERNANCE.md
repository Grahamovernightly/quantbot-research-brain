# QuantBot Research Brain — Governance

> This repository is the institutional memory of the QuantBot quant research operation.
> It is written for AI agents and human operators alike.
> Every significant discovery, decision, and evolution is recorded here.
> Future agents: read RESEARCH_STATE.md first, then the relevant discovery docs.

## Principles

1. **Evidence over intuition.** Every parameter choice should have a data source.
2. **Record failures as carefully as wins.** A failed hypothesis saves future compute.
3. **Gate passes are not the goal.** Live P&L is the goal. Gates are the filter.
4. **The kill switch changes the math.** Standard risk thresholds don't apply when you have a hard external circuit breaker at 4.8% DD.
5. **Regime first, parameters second.** The best parameters for a ranging market are wrong for a trending one.
6. **Don't bin outliers.** Magic 777 looked "dangerous" in backtests. It made $25k live. Investigate before discarding.

## Repository Structure

```
discoveries/     — What we found and why it matters (immutable once written)
candidates/      — Specific candidate profiles worth preserving
playbook/        — Strategic frameworks and deployment logic
state/           — Living document: current research phase and findings
intelligence/    — Batch-level insights from backtest runs
```

## How to Update

- **After each significant discovery:** add a file to `discoveries/`
- **After each research batch:** update `intelligence/BACKTEST_INSIGHTS.md`
- **After each gate pass or FT promotion:** update `candidates/APPROVED_PROFILES.md`
- **Every 24-48 hours:** update `state/RESEARCH_STATE.md`
- **After major decisions:** add an entry to the Decision Log below

## Decision Log

| Date | Decision | Rationale | Agent |
|------|----------|-----------|-------|
| 2026-04-07 | Created this repo | Need persistent cross-session intelligence ledger | Hermes |
| 2026-04-07 | Blueprint_EA built from GRIDKEEPER spec | POW Banker encrypted, clean-room reimplementation gives full parameter control | Hermes+Claude |
| 2026-04-07 | Weekend close default=false | Empirical data: holding through weekends better 77-100% of the time for grid EAs | Hermes |
| 2026-04-07 | Three EA families defined | Different market regimes and account types need different parameter profiles | Hermes |
| 2026-04-07 | BLUEPRINT_AGGRESSIVE gate profile created | Standard gates reject best performers due to grid EA trade frequency characteristics | Hermes+Claude |
| 2026-04-07 | min_per_month lowered to 0.5 | Basket-close grids trade ~1 sequence/6-8 weeks; standard threshold calibrated for signal EAs | Hermes |
