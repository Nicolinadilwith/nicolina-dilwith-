# Perfect Competition Brief

## Problem

We need to find the most profitable combination of vegetables by taking into account:

Season & farm

WEEKS = 36 (season length)
TOTAL_BED_CAP = 64 total beds (16 beds × 4 plots)

Fixed costs

FARMER_SALARY = $50,000/season — paid regardless of hours actually used
FIXED_COSTS_OTHER = $20,000/season — overhead
($70,000 combined, sunk either way — irrelevant to the planting decision itself, only to whether the farm is profitable overall)

Labor available

FARMER_FIELD_HOURS = 720 hrs — the farmer's own capacity, already paid for by her salary
TEMP_WORKER_HOURS = 1,440 hrs per worker, in whole blocks
TEMP_WORKER_COST = $25,000 per worker, per block (not a continuous rate)
MAX_TEMP_WORKERS = 4 — the most temp labor the farm can hire

Prices (fixed because the farm is a price-taker — perfect competition)

Crop	Price/bed
Tomatoes	$8,800
Carrots	$2,094
Mesclun	$2,700

Bed caps (physical limit per crop, plus the farm-wide cap above)

Crop	Max beds
Tomatoes	20
Carrots	20
Mesclun	30

To summarize the problem: 
Fixed = season, costs, prices, caps, labor supply. 
Chosen = the three bed counts (workers hired follows automatically). 
Limits = bed caps and the worker ceiling exist but aren't what bind at the optimum — it's marginal economics that stops each crop, for two different underlying reasons.
We would like to find the most profitable amount of each crop to plant.

I hypothesize that the most profitable combination of beds will be 7 beds of tomatoes, 18 beds of carrots, and 22 beds of mesclun, for a total of 47 beds. This combination should produce the highest profit because it balances the relatively high price of tomatoes with the lower labor requirements and slower diminishing returns of carrots and mesclun.

> **AI note, added after the analysis:** this hypothesis leaves 17 of 64 beds idle, which is a strong claim — it can only hold if the farm has run out of labor at 47 beds, or if the next bed of every crop costs more to grow than it earns. Neither is true here. At 7/18/22 the farm needs about 2,651 hours of temp labor, well under the 5,760-hour cap the farm can buy (equivalent to 4 full-time temp workers) — nowhere near a binding labor limit. And the actual analysis (see `analysis/figures/Nicolina-Perfect Competition Memo and Reflection.docx`) shows the opposite of "next bed costs more than it earns": 13 more beds (3 more tomatoes, 2 more carrots, 8 more mesclun, for 60 of 64 — the full 20- and 30-bed caps on carrots and mesclun) were still profitable to add, raising profit from $34,233 to $42,762. So the 17 idle beds in this hypothesis weren't derived from either mechanism — they came from an intuitive guess made before running the labor-hours engine, and the guess undershot on every crop.

The 7 tomatoes / 18 carrots / 22 mesclun = 47 beds (17 idle) figure is the pre-analysis hypothesis — a guess made before the labor-hours engine was ever run.

The model's actual recommendation is 10 tomatoes / 20 carrots / 30 mesclun = 60 of 64 beds (only 4 idle), profit $42,762.

How I know I was wrong:

Recomputing the hypothesis's own numbers: at 7/18/22, the farm needs about 2,651 hours of temp labor against a 5,760-hour cap — nowhere near a point where any crop's next bed costs more than it earns (we know that because the model shows 13 more beds were worth planting). This guess was too conservative on every crop, leaving $8,529 on the table ($42,762 − $34,233). It wasn't derived from either mechanism — it was an intuitive guess that turned out to undershoot.

Why the real answer — 4 idle beds at 60/64 — does hold up:

Tomatoes stop at 10 (cap is 20). Bed 11's own marginal cost is $9,391 ($8,511 in labor + $880 fertilizer) against an $8,800 price — a straightforward loss, pricing labor by the hour. Diminishing returns catches up with tomatoes specifically because their HRS_PER_BED (2.5) and DIM_PCT (10%/bed) are both far higher than the other two crops.

Carrots and mesclun don't stop early — they go all the way to their 20- and 30-bed caps. Priced by the hour, carrot bed 20 still earns about $406 at the margin, and mesclun bed 30 about $280. Neither crop's own marginal cost ever catches up to its price within its cap, so it's the physical bed caps — not the economics — that stop them.
