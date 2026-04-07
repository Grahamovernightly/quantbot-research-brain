# FT Deployment Playbook
*Written: 2026-04-07 | Author: Hermes*
*Status: AUTHORITATIVE — follow this exactly*

---

## The Problem This Solves

The FT deployment process has historically been ad-hoc, resulting in:
- 31 "phantom" candidates (backend says forward_test, no chart on master)
- 23 candidates on chart but NOT in copier (trading with no copy anywhere)  
- 4 candidates dropped by the 64-chart MT5 limit
- No automated verification that deployment actually worked
- No systematic retirement of underperformers

This playbook defines the complete lifecycle from risk_approved → deployed → 
monitored → retired or promoted to stack.

---

## Architecture (correct understanding)

```
MT5Suite (Railway)
  ↓ mt5suite-sync edge function (Supabase cron)
Supabase candidates_current table
  ↓ NC dashboard reads
Nerve Centre dashboard (shows all states including risk_approved)

ForexVPS master terminal (account 52760131 ICMarkets)
  ↓ trade copier polls master positions
Trade Copier
  ↓ applies magic_filter per slave
Slave prop firm terminals (BrightFunded, FTMO, GoatFunded etc)
```

The copier does NOT decide which candidates to copy based on MT5Suite state.
It copies based on:
1. Which magic numbers are active on the master terminal (EAs loaded on charts)
2. Which magic numbers pass the slave's magic_filter (if any — BrightFunded/FTMO 
   have no filter, they copy everything the master trades)

So "deploying to FT" requires TWO separate steps:
1. Load the EA on a chart on the master terminal with the correct magic number
2. The copier automatically picks it up — no copier config change needed
   (unless the slave has a magic_filter, in which case add the magic to it)

---

## Constraints

- **MT5 chart limit: 64 charts per terminal** — hard limit, charts beyond 64 
  are loaded in config but not active (the "dropped" chart problem)
- **Master terminal slots:** Currently using ~60+ charts. Need to cull before 
  adding new ones.
- **Second master terminal option:** Opening a second MT5 instance on ForexVPS 
  with a separate copier slave chain would double FT capacity to 128 slots.
  Recommended when Blueprint EA candidates start accumulating at scale.

---

## Step 1: Pre-Deployment Checklist

Before deploying any new FT candidate:

```
[ ] Candidate is at risk_approved state in MT5Suite
[ ] Candidate has been evaluated with BLUEPRINT_AGGRESSIVE gate profile 
    (ea_profile_id=10) if it's a Blueprint EA or grid EA
[ ] Chart count on master is < 60 (leave headroom for 64-chart limit)
[ ] Magic number is unique — not already used on another chart
[ ] Set file exists with correct parameters matching the backtest
[ ] If adding to a slave with magic_filter — update the filter
```

---

## Step 2: Deployment

### On ForexVPS master terminal (account 52760131)

1. Open MetaTrader 5 master terminal
2. Open new chart for the symbol (e.g. USDCAD M1)
3. Attach the EA (POW_Banker_EA.ex5 or Blueprint_EA.ex5)
4. Load the set file from the backtest
5. **Verify MAGIC_NUMBER in the set file matches the candidate's magic_number 
   in MT5Suite** — this is the critical link
6. Enable AutoTrading
7. Confirm the EA initialises without errors
8. Note the chart number and save the profile

### Verification (within 1 hour):
- Check that magic number appears in `list_magics.py` output on ForexVPS
- Check that trades start appearing in Supabase trade_history within first 
  sequence open (may take hours/days for first trade)
- Check mt5suite-sync runs and updates candidates_current

---

## Step 3: Post-Deployment Monitoring (daily cron)

Daily cron on Hetzner checks for deployment drift:

```python
# Pseudo-code for daily FT deployment monitor
for each candidate in MT5Suite with state=forward_test:
    is_on_master = magic_number in master_active_magics_last_7d
    is_in_copier = magic_number in copier_active_magics (polled from ForexVPS)
    
    if not is_on_master:
        alert("PHANTOM: #{id} {symbol} magic={magic} - in MT5Suite FT but not on master")
    
    if is_on_master and not is_in_copier:
        alert("ORPHAN: #{id} - on master but not being copied")
    
    if is_on_master and trade_count_last_30d == 0:
        if days_since_deployment > 30:
            alert("STALE: #{id} - deployed 30+ days, zero trades")
```

---

## Step 4: Weekly Performance Review

Every Sunday (add to Hetzner cron, or triggered by ft_retirement_evaluator.py):

### Retire criteria (mark as retired in MT5Suite + remove from chart):
- Zero trades after 60+ days on master
- Net P&L < -$200 in last 30 days (actively losing)
- Known-bad EAs: Turtle, Silver ORB (contract size issue)
- Duplicate of better-performing candidate on same symbol/EA

### Promote to stack criteria:
- 30+ days live, trade_count > 5, net P&L > 0
- No single loss > kill_threshold% of account
- L2 data available (equity CSV exists)
- Run through challenge simulator before adding to any copier magic_filter

### Stack addition process:
1. Run L2 simulation with candidate added to current stack
2. If pass rate improves or stays same with faster days: add to magic_filter
3. Document multiplier recommendation in research brain
4. Deploy to relevant slaves via copier config update

---

## Current FT Status (2026-04-07)

From Claude's audit:

| Status | Count | Action |
|--------|-------|--------|
| On chart + in copier (fully deployed) | 15 | Keep, monitor |
| On chart, NOT in copier | 23 | Review — orphans, may be fine if trading |
| On chart but DROPPED (>64 limit) | 4 | Fix order.wnd, restore C10143/13604/13668 |
| NOT on any chart (phantom) | 31 | Do NOT retire blindly — classify first |
| HAS_EXPERT charts (unidentified) | 28 | Identify magic param name |

### Phantom classification rule:
Before retiring any phantom:
1. Check if it ever appeared in trade_history (has it ever traded?)
2. If yes and profitable → was deployed correctly, then removed. Worth redeploying.
3. If yes and losing → legitimate retirement
4. If never traded → was never properly deployed. Do not count as "tried and failed".
   These should be redeployed or consciously parked, not retired.

High-value phantoms worth redeploying:
- #16862 EURJPY PF=53.76 (on chart09 but not in copier)
- #3004 EURUSD PF=32.73 (not on any chart)
- #16972 USDCAD PF=9.09
- #16072 EURJPY PF=8.62

Low-value phantoms to park (not retire, not deploy):
- All CADCHF POW Banker (8 candidates, PF 3-4.7)
- All NightRevert AUDNZD/EURCHF (zero trades, low PF)
- All Dual_Thrust (PF=0.0, never backtested properly)
- CFC USDCAD 21915/21921

---

## Second Master Terminal Plan

When Blueprint EA candidates accumulate (target: 20+ ready for FT):

1. Launch a second MT5 instance on ForexVPS
   - New terminal directory (e.g. C:\MT5_Master2\)
   - Same ICMarkets account or new demo account
   - Same EA set running in parallel

2. Add second master to copier config:
   ```yaml
   masters:
     - id: master_1
       account: 52760131
       ...
     - id: master_2  
       account: [new account]
       ...
   ```

3. Split candidates across masters:
   - Master 1: existing POW Banker + top Blueprint
   - Master 2: Blueprint overflow + experimental

4. Each slave can be configured to copy from one or both masters

This doubles FT capacity to ~128 slots total.

---

## Cron Schedule for FT Lifecycle

Add to Hetzner crontab:

```cron
# Daily FT deployment monitor (07:00 UTC)
0 7 * * * /usr/bin/python3 /home/openclaw/quantbot-scripts/ft-automation/ft_deployment_monitor.py >> /home/openclaw/logs/ft_deployment_monitor.log 2>&1

# Weekly FT performance review (Sunday 06:00 UTC)  
0 6 * * 0 /usr/bin/python3 /home/openclaw/quantbot-scripts/ft-automation/ft_weekly_review.py >> /home/openclaw/logs/ft_weekly_review.log 2>&1
```

Both scripts need to be built. Inputs:
- ForexVPS master terminal active magics (via MT5 API or list_magics.py)
- MT5Suite FT candidates (via API)
- Supabase trade_history (30-day window)
- Research brain ledger for context

Outputs:
- Telegram alert for phantoms, orphans, stale candidates
- Weekly Telegram report: top performers, retirement recommendations, stack additions
- GitHub commit to research brain with updated state

---

## Blueprint EA FT Deployment (when ready)

Blueprint EA candidates need:
1. Blueprint_EA.ex5 deployed to master terminal (not yet done)
2. Set file generated from the candidate's backtest parameters
3. Magic number matching the candidate record in MT5Suite
4. EquityLogger active (now built) — L2 CSV will auto-generate

The ft_slot_manager.py script handles the technical deployment.
It needs to be updated to support Blueprint_EA.ex5 as a deployment target.
Currently it only knows about POW_Banker_EA.ex5 and NightRevert_v0.ex5.
