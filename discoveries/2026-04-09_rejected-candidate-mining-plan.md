# Rejected Candidate Mining Plan
*Created: 2026-04-09 | Agent: Hermes*

## Why this exists

MT5Suite has ~25k rejected candidates. Magic 777 demonstrates that rejection does NOT imply lack of edge.
Some candidates were rejected because the old governance stack penalised exactly the behaviors that aggressive grid challenge-passers need:
- low basket-close trade counts
- long sequence duration
- high consecutive losses despite bounded external kill-switch risk
- family-level signal not yet recognised

The objective is to mine the rejected pool systematically rather than by luck.

## Two-Lane Agenda

### Lane A — Challenge Fast
Goal: pass challenges quickly.

Bias toward:
- very high PF / payout speed
- acceptable kill-switch-bounded risk
- symbols/families already proven live or near-live
- tolerate higher DD if kill-switch math still works

Examples:
- Magic 777 / 7771 / 7772 / 7773 family
- aggressive USDCAD / selective GBPUSD families
- future high-PF Blueprint aggressive families

### Lane B — Funded Safe
Goal: low-touch autopilot extraction over long periods.

Bias toward:
- lower DD structural mean reversion
- steady but slower income
- cleaner symbol families
- lower concentration risk

Examples:
- CADCHF family
- AUDNZD / AUDCAD / EURCHF structural families
- safer Blueprint translations of proven Banker logic

## Core principle

Do NOT score all rejected candidates with one universal metric.
First classify each rejected candidate into a lane hypothesis:
- challenge-fast
- funded-safe
- discard/noise

## Phase 1 — Build a triage table for all rejected candidates

For every rejected candidate, compute/store:
- candidate_id
- symbol
- ea_name / family
- state / rejection stage / rejection reason
- profit_factor
- max_drawdown_pct
- total_trades
- max_consecutive_losses
- parameter_hash
- created_at / updated_at
- if available: deployment_status, forward_test_start, magic_number
- if available: work-item planner_mode / batch_id / parameter payload

Add derived fields:
- lane_guess
- rejection_pattern
- family_guess
- review_priority

## Phase 2 — Partition by rejection reason

Bucket rejected candidates into the reasons that matter:

### Bucket A — likely hidden gold
Candidates rejected mainly because of governance mismatch, not bad economics:
- min_trades failure with PF >= 2.0
- max_consecutive_losses failure with strong PF and bounded DD
- duration / sequence-count mismatch for grid EAs
- duplicate / historical cleanup cases where family remains interesting

### Bucket B — near-miss review
Candidates with:
- PF 1.90–1.99
- OR low-DD structural family scores with PF 1.60–1.89
- OR strong live-family resemblance (e.g. CADCHF cluster translations)

### Bucket C — probable noise
Candidates with:
- poor PF
- poor DD
- no family reinforcement
- no live resemblance

## Phase 3 — Family-first mining, not candidate-first mining

Mine rejected candidates by family clusters.

Priority families now:
1. Magic 777 / Banker aggressive family
2. USDCAD aggressive family
3. CADCHF structural family
4. AUDNZD structural family
5. AUDCAD structural family
6. EURCHF structural family
7. GBPUSD aggressive near-miss family

Within each family, rank by:
- repeated parameter neighbourhood success
- live relevance
- challenge vs funded fit
- kill-switch-adjusted risk

## Phase 4 — Challenge-fast review rules

Promote for closer investigation if:
- PF >= 2.0 and rejection came from trade-count / streak logic
- OR candidate resembles known 777-style winners
- OR near-miss PF with very high earnings velocity and kill-switch-bounded risk

Required closer-investigation steps:
1. extract exact params
2. compare against known live winner family params
3. collect / inspect L2 if available
4. run challenge-stack sim with kill switch assumptions
5. decide: FT candidate / challenge candidate / discard

## Phase 5 — Funded-safe review rules

Promote for closer investigation if:
- low-DD structural family cluster exists
- repeated PF 1.5–1.9 appears across many nearby candidates
- parameters generalise to similar structural pairs

Required closer-investigation steps:
1. cluster by parameter neighbourhood
2. identify stable LP/PS and DTS/TS patterns
3. run translations on structural cousin symbols
4. decide: funded family seed / FT probe / discard

## Immediate execution order

### Wave 1 — do now
1. Deep-dive Magic 777 family causally
2. Mine rejected USDCAD + GBPUSD Banker aggressive families for challenge-fast lane
3. Continue CADCHF family exploitation and structural cousin translation

### Wave 2
4. Mine rejected AUDNZD / AUDCAD / EURCHF structural families
5. Compare winning CADCHF neighbourhood against rejected cousins to learn what breaks generalisation

### Wave 3
6. Broader rejected-pool lane classification across all symbols
7. Build a durable shortlist table for recurring manual review

## Operational implementation suggestion

Create a recurring Hermes-led review process:
- query latest rejected candidates in batches
- classify into challenge-fast / funded-safe / discard
- surface top 5 per family
- save durable shortlist to research brain
- only escalate a small number to deep review / L2 collection / FT

## Success metric

The process is working if it consistently produces:
- challenge-fast candidates that pass under kill-switch-aware logic
- funded-safe structural families with repeatable low-DD behavior
- fewer random sweeps and more family compounding
