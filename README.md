# QuantBot Research Brain

> Institutional memory for the QuantBot quant research operation.
> Built by Hermes. For agents and humans alike.

## Start Here

1. **`state/RESEARCH_STATE.md`** — What's happening right now. Read this first.
2. **`GOVERNANCE.md`** — Principles, decisions, who did what and why.
3. **`discoveries/`** — Key findings that changed how we think.
4. **`candidates/APPROVED_PROFILES.md`** — Best candidates found so far.
5. **`playbook/`** — Strategic frameworks for deployment.
6. **`intelligence/`** — Batch-level learnings from backtest runs.

## What This Is Not

This is not code. This is not a dashboard. This is the **reasoning layer** —
the record of hypotheses tested, discoveries made, and decisions taken.
The code lives in Blueprint_EA repo. The pipeline lives in mt5-suite.
The brain lives here.

## Quick Context

- **Blueprint EA** — clean-room reimplementation of POW Banker EA (bidirectional grid)
- **Three families** — STRUCTURAL (funded), SESSION (challenge), OPPORTUNIST (regime-gated)
- **Research factory** — 6 Kamatera workers running OHLC backtests 24/7
- **Target** — a family of gate-passing, robustness-certified, kill-switch-compatible EAs
- **The kill switch changes everything** — 4.8% DD hard stop means risk math differs from standard

## Repos
- `Grahamovernightly/Blueprint_EA` — the EA code
- `Grahamovernightly/mt5-suite` — pipeline API and gates
- `Grahamovernightly/quantbot-scripts` — research factory dispatchers
- `Grahamovernightly/quantbot-research-brain` — this repo (you are here)
