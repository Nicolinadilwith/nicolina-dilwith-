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
- `FARMER_RATE = FARMER_SALARY / FARMER_TOTAL_HOURS ≈ $34.72/hr` — her implied hourly rate,
  multiplied against her field hours in Convention A below to get the labor cost the crop P&L
  actually carries (see Convention A step 2) — not her full salary
- `TEMP_WORKER_HOURS = 1,440` hrs per worker per season
- `TEMP_WORKER_COST = $25,000` per worker per season
- `TEMP_RATE = TEMP_WORKER_COST / TEMP_WORKER_HOURS ≈ $17.36/hr` — the continuous per-hour rate
  temp labor is costed at in Convention A; temp labor is bought by the hour, not hired in discrete
  worker-sized blocks (see Convention A step 3)
- `MAX_TEMP_WORKERS = 4` — caps how many hours of temp labor are available at all:
  `MAX_TEMP_HOURS = MAX_TEMP_WORKERS × TEMP_WORKER_HOURS = 5,760` hrs. This bounds capacity, not
  cost — see Constraints.
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
per-crop allotment. Both the farmer's hours and temp hours are priced continuously, per hour —
neither is a lump paid regardless of how much of it is used.

1. `TOTAL_LABOR_HRS = Σ_c LABOR_HRS(q_c, c)` — summed across all three crops.
2. `FREE_HRS_USED = MIN(TOTAL_LABOR_HRS, FARMER_FIELD_HOURS)`, and the farm's cost for it is
   `FARMER_LABOR_COST = FREE_HRS_USED × FARMER_RATE`. In every plan worth evaluating, total demand
   exceeds 720 hours, so this is `FARMER_FIELD_HOURS × FARMER_RATE = $25,000` — the value of her
   field labor at her own implied rate, not her full $50,000 salary. Her salary pays for 1,440
   hours of which only half are field hours; only the field-labor half is a cost of growing crops,
   the other half is outside this P&L.
3. `PAID_HRS_NEEDED = MAX(0, TOTAL_LABOR_HRS − FARMER_FIELD_HOURS)` — hours beyond the farmer's
   free allowance, bought continuously by the hour at `TEMP_RATE`, not hired in discrete
   worker-sized blocks.
4. `TEMP_LABOR_COST = PAID_HRS_NEEDED × TEMP_RATE`.

Then:

```
REVENUE    = Σ_c q_c × PRICE[c]
FERTILIZER = Σ_c q_c × FERT_COST[c]
PROFIT_A   = REVENUE − FERTILIZER − FARMER_LABOR_COST − TEMP_LABOR_COST − FIXED_COSTS_OTHER
```

`PROFIT_A` is the objective function.

### Convention B — Blended-rate costing (reporting only, never the objective)

Restates the same cash spend as a single uniform $/hr rate, for per-bed unit-economics reporting.
The blend is a **farm-level fact** — one rate for the whole farm, computed once — not something
recomputed per crop.

```
TOTAL_LABOR_$          = FARMER_LABOR_COST + TEMP_LABOR_COST    (same cash as Convention A)
TOTAL_LABOR_HRS_BOUGHT = FREE_HRS_USED + PAID_HRS_NEEDED         (= TOTAL_LABOR_HRS)
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
- `PAID_HRS_NEEDED ≤ MAX_TEMP_HOURS` (5,760 hrs) — a plan needing more temp labor than that is
  infeasible, not merely more expensive. This bounds available hours; it says nothing about how
  those hours are priced (see Convention A).

## Objective

Maximize `PROFIT_A` over `(Q_TOMATOES, Q_CARROTS, Q_MESCLUN)` subject to the constraints above.

## Marginal cost behavior (mechanism, not shape)

Marginal cost of the `q`-th bed of crop `c` is driven by two mechanisms that can pull against each
other bed to bed:

1. **Compounding labor requirement.** `LABOR_HRS(q, c) − LABOR_HRS(q−1, c)` grows with `q` because
   of the `(1 + DIM_PCT[c])^q` term — each additional bed needs more marginal hours than the one
   before it, in isolation.
2. **A one-time price change in the marginal hour, not a recurring one.** Every hour up to
   `FARMER_FIELD_HOURS` (720, farm-wide) is already paid for — the farmer's field-labor cost is a
   flat `$25,000` regardless of how those hours are split across crops — so a bed drawing on that
   allowance costs only its fertilizer at the margin. Once the farm-wide total crosses 720 hours,
   every additional hour costs `TEMP_RATE` (~$17.36/hr) continuously — there is no further step,
   because temp labor is bought by the hour, not hired in worker-sized blocks (see Convention A).
   So the marginal price of labor drops once, from the farmer's flat allowance to a continuous paid
   rate, and stays there.

Mechanism 1 pushes marginal cost up throughout; mechanism 2 produces one drop when the farmer's
free hours run out mid-crop, not a repeating one. Their sum is **not guaranteed to rise
monotonically** near that crossing point — do not hardcode or assume "marginal cost increases with
`q`" anywhere in the model or its checks. Derive `PROFIT_A(q) − PROFIT_A(q−1)` from the formulas
above and let the shape fall out empirically, per crop, before drawing conclusions about where a
crop stops being profitable at the margin. Because labor is priced continuously with no discrete
worker-block steps, a crop's own marginal cost crossing its price is a real, decisive signal in
this model — unlike a lumpy-labor version of the model, there is no separate "not worth hiring a
whole extra block for a few more beds" effect layered on top.
