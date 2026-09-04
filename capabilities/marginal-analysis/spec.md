# Spec: Perfect Competition Farm — Profit-Maximizing Bed Allocation

Written before/independent of any particular spreadsheet build. States the model's logic — named
parameters and formulas — not cell addresses, so it could be built from this document without
seeing the workbook.

## Purpose

Given three crops (tomatoes, carrots, mesclun) and a farm that is a price-taker (perfect
competition — price per bed is fixed, not set by the farm), choose the integer number of beds of
each crop that maximizes seasonal profit, subject to bed and labor-force limits.

## Decision variables

`Q_TOMATOES`, `Q_CARROTS`, `Q_MESCLUN` — integer beds planted in each crop, each `≥ 0`.

Generically, `q` denotes beds planted in crop `c`, for `c ∈ {TOMATOES, CARROTS, MESCLUN}`.

## Parameters — per crop (given)

| Name              | Tomatoes | Carrots | Mesclun |
|-------------------|---------:|--------:|--------:|
| `BED_CAP[c]`      |       20 |      20 |      30 |
| `PRICE[c]` ($/bed)|    8,800 |   2,094 |   2,700 |
| `HRS_PER_BED[c]` (hrs/wk/bed) | 2.5 | 0.833 | 1.25 |
| `FERT_COST[c]` ($/bed) |    880 |     440 |     880 |
| `DIM_PCT[c]` (%/bed)  |     10% |    2.5% |   1.25% |

## Parameters — farm-wide (given)

- `WEEKS = 36` — season length
- `TOTAL_BED_CAP = 64`
- `FARMER_SALARY = $50,000` /season, fixed — paid whether or not it's fully used
- `FARMER_TOTAL_HOURS = 1,440` hrs/season
- `FARMER_FIELD_SHARE = 50%`
- `FARMER_FIELD_HOURS = FARMER_TOTAL_HOURS × FARMER_FIELD_SHARE = 720` hrs — the farmer's own
  field labor capacity, already paid for by her salary
- `FARMER_RATE = FARMER_SALARY / FARMER_TOTAL_HOURS ≈ $34.72/hr` — an implied rate for reference;
  it is never multiplied against anything in Convention A below, since her salary is a fixed cost
  regardless of hours worked
- `TEMP_WORKER_HOURS = 1,440` hrs per worker per season
- `TEMP_WORKER_COST = $25,000` per worker per season — a discrete block, not a per-hour rate
- `TEMP_RATE = TEMP_WORKER_COST / TEMP_WORKER_HOURS ≈ $17.36/hr` — an implied rate, used
  continuously only in Convention B and the isolated-crop marginal-cost check below; never used as
  a continuous rate in Convention A's cash cost
- `MAX_TEMP_WORKERS = 4`
- `FIXED_COSTS_OTHER = $20,000` /season — non-labor overhead

## The engine: labor-hours formula

This one formula drives the whole model. For crop `c` planted at `q` beds:

```
LABOR_HRS(q, c) = q × HRS_PER_BED[c] × WEEKS × (1 + DIM_PCT[c])^q
```

Specify it exactly this way — not `q × HRS_PER_BED[c] × WEEKS`, and not any other variant.

**Why the `(1 + DIM_PCT[c])^q` term is required, not optional.** Strip it out and `LABOR_HRS` is
linear in `q`: every bed costs the same labor as the last, marginal cost of labor is flat, and the
model has no economic story to tell about why a farm wouldn't plant its most profitable crop in
every available bed. The exponential term is diminishing returns to labor made computable: each
additional bed of a crop raises the per-bed labor requirement of *every* bed of that crop — pest
pressure spreads, harvest windows collide, walking distance grows. That mechanism is what can make
marginal cost climb and is why "plant the whole farm in tomatoes" can be a mistake rather than an
obvious win — see Marginal Cost Behavior below for what this does and doesn't guarantee.

## Labor cost allocation — two conventions

Both conventions must be specified. Specifying only one is the most common structural defect in
this model.

### Convention A — Cash / marginal costing (drives the objective)

This is what the optimizer maximizes. Labor capacity is filled in a fixed order: **the farmer's
own hours are consumed first, always**, and that allowance is a farm-wide resource — not a
per-crop allotment.

1. `TOTAL_LABOR_HRS = Σ_c LABOR_HRS(q_c, c)` — summed across all three crops.
2. `FREE_HRS_USED = MIN(TOTAL_LABOR_HRS, FARMER_FIELD_HOURS)`
3. `PAID_HRS_NEEDED = MAX(0, TOTAL_LABOR_HRS − FARMER_FIELD_HOURS)`
4. `WORKERS_NEEDED = ROUNDUP(PAID_HRS_NEEDED / TEMP_WORKER_HOURS, 0)` — temp workers are hired in
   whole, discrete blocks of `TEMP_WORKER_HOURS`, never fractionally and never continuously by the
   hour.
5. `WORKERS_HIRED = WORKERS_NEEDED`, subject to `WORKERS_HIRED ≤ MAX_TEMP_WORKERS` — a hard
   feasibility constraint on the plan (see Constraints), not a cap that silently discards need.
6. `TEMP_LABOR_COST = WORKERS_HIRED × TEMP_WORKER_COST` — a step function of `TOTAL_LABOR_HRS`,
   not `PAID_HRS_NEEDED × TEMP_RATE`. Hiring a worker costs the full block whether she is needed
   for 1 hour or 1,440.

Then:

```
REVENUE    = Σ_c q_c × PRICE[c]
FERTILIZER = Σ_c q_c × FERT_COST[c]
PROFIT_A   = REVENUE − FERTILIZER − FARMER_SALARY − TEMP_LABOR_COST − FIXED_COSTS_OTHER
```

`PROFIT_A` is the objective function.

### Convention B — Blended-rate costing (reporting only, never the objective)

Restates the same cash spend as a single uniform $/hr rate, for per-bed unit-economics reporting.
The blend is a **farm-level fact** — one rate for the whole farm, computed once — not something
recomputed per crop.

```
TOTAL_LABOR_$          = FARMER_SALARY + TEMP_LABOR_COST        (same cash as Convention A)
TOTAL_LABOR_HRS_BOUGHT = FARMER_FIELD_HOURS + (WORKERS_HIRED × TEMP_WORKER_HOURS)
BLENDED_RATE            = TOTAL_LABOR_$ / TOTAL_LABOR_HRS_BOUGHT
```

Each crop's allocated labor cost is its own hours times that single farm-wide rate:

```
LABOR_COST_ALLOCATED(c) = LABOR_HRS(q_c, c) × BLENDED_RATE
PROFIT_B = REVENUE − FERTILIZER − Σ_c LABOR_COST_ALLOCATED(c) − FIXED_COSTS_OTHER
```

`PROFIT_B` must equal `PROFIT_A` in total (same underlying cash), even though Convention B
allocates labor cost to individual crops and Convention A does not. Do not compute a separate
blended rate per crop, and do not let Convention B's per-crop allocation feed back into the
Convention A optimization.

## Constraints

- `0 ≤ q_c ≤ BED_CAP[c]` for each crop, integer.
- `Q_TOMATOES + Q_CARROTS + Q_MESCLUN ≤ TOTAL_BED_CAP`
- `WORKERS_NEEDED ≤ MAX_TEMP_WORKERS` — a plan requiring more than 4 temp workers is infeasible,
  not merely more expensive.

## Objective

Maximize `PROFIT_A` over `(Q_TOMATOES, Q_CARROTS, Q_MESCLUN)` subject to the constraints above.

## Marginal cost behavior (mechanism, not shape)

Marginal cost of the `q`-th bed of crop `c` is driven by two mechanisms that can pull against each
other bed to bed:

1. **Compounding labor requirement.** `LABOR_HRS(q, c) − LABOR_HRS(q−1, c)` grows with `q` because
   of the `(1 + DIM_PCT[c])^q` term — each additional bed needs more marginal hours than the one
   before it, in isolation.
2. **Discrete labor-supply steps.** Whether those marginal hours cost anything in cash depends on
   whether the farm-wide 720-hour free allowance is already exhausted, and whether the current
   temp-worker block (1,440 hrs, $25,000) still has slack in it. A bed that lands just after a new
   worker is hired can be nearly free at the margin (the block is already paid for); a bed that
   lands just as a block runs out triggers the next full $25,000 step.

Mechanism 2 is a step function and mechanism 1 is smooth and compounding, so their sum is **not
guaranteed to rise monotonically** — do not hardcode or assume "marginal cost increases with `q`"
anywhere in the model or its checks. Derive `PROFIT_A(q) − PROFIT_A(q−1)` from the formulas above
and let the shape fall out empirically, per crop, before drawing conclusions about where a crop
stops being profitable at the margin.

An isolated-crop marginal-cost view — each crop evaluated as if it alone had first claim on the
full 720 free hours, with temp hours costed continuously at `TEMP_RATE` rather than in discrete
blocks — is useful for auditing the engine formula in isolation (e.g. a hand-calculated check at
`q = 1`), but it is not Convention A and must not be mistaken for the farm's real per-crop cost:
the free hours and the temp-worker blocks are shared, farm-level resources, consumed once across
all three crops together.
