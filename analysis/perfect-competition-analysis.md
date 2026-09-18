---
type: analysis
engagement: perfect-competition
capability: marginal-analysis
date: 2026-09-18
---

# Perfect competition — analysis

## 1. Why tomatoes stop at ~10 beds despite being the money crop

Revenue per bed ($8,800 for tomatoes) is a constant price, and it doesn't change no matter how many beds you plant. Marginal cost is the opposite and the cost of the next bed specifically, and in this model it rises steeply as you plant more tomato beds, for two compounding reasons baked into the Inputs sheet.

Tomatoes have a "diminishing returns" rate of 10% per bed — the highest of the three crops (carrots are 2.5%, four times lower). In this model that shows up as each additional tomato bed needing more labor hours than the last.

The farmer only has 720 hours of "free" field time before any paid labor kicks in, and tomatoes burn through that allotment fast because each bed takes an increasing amount of it. The farmer's free hours run out at bed 5. From bed 6 onward, every hour of that rising labor requirement is paid at the temp-worker rate ($17.36/hr). Since the hours needed per bed are themselves growing, the dollar cost per additional bed grows even faster.

Tracing the actual marginal cost column bed by bed shows the crossing directly:

Bed 9 costs about $7,244 to add — still comfortably under the $8,800 price, earning about $1,556 of marginal profit. Bed 10 costs $8,248.59 — still under price, but only by $551. Bed 11 costs $9,390.72 — now above the $8,800 price, so planting it would lose about $591. That's the exact crossing point you described: marginal cost sits below $8,800 through bed 10 and above it at bed 11, so a profit-maximizing farmer plants exactly through bed 10 and stops, regardless of the fact that 20 beds are allowed.

That's the whole mechanism of P = MC for a price-taking producer: price is fixed by the market and acts as marginal revenue, so the profit-maximizing quantity is wherever the rising marginal-cost curve meets that fixed price line — not wherever revenue-per-unit happens to be highest. Carrots make the contrast obvious: their price is only $2,094, a quarter of tomatoes', but because their diminishing-returns rate is so much gentler (2.5% vs 10%), their marginal cost is still comfortably below price even at bed 20, the cap. Carrots aren't stopped by economics at all — they're stopped by running out of allowed ground (the sheet even prices bed 21 at roughly $353 of profit it's leaving on the table). Tomatoes are the mirror image: high price, but a marginal cost curve that outruns even that high price by bed 11, so they're self-limiting well inside their cap. Being the best per-bed earner sets how high the bar is; it says nothing about how many beds it's worth clearing that bar for.

## 2. Which constraints bind, and what relaxing one is worth

Carrots and mesclun are cap-limited: their marginal cost is still comfortably below price at the last bed the cap allows (bed 20 for carrots, bed 30 for mesclun), so nothing in the economics tells them to stop, just the 20-bed and 30-bed caps. Bed 21 of carrots would earn $352.49 in profit, bed 31 of mesclun would earn $246.47. Those are shadow prices in the strict LP sense, the value of loosening a binding constraint by one unit, and they're directly usable: if you could rent or convert one more bed of ground for tomatoes into carrot/mesclun ground, it's worth paying up to $352 or $246 for it, respectively. Tomatoes, by contrast, stop on economics alone at bed 10, so its bed cap isn't binding and has no shadow price. More tomato ground is worth $0 to this plan.

The other two constraints in the model, total beds (64) and temp labor hours (4 workers × 1,440 hrs = 5,760 hrs) both sit with slack at the optimum: 60 of 64 beds used, and about 5,277 of 5,760 labor-hours used (~483 hours to spare). Neither is what's stopping any crop, so their shadow price is $0. Paying for a bigger plot or a 5th temp worker wouldn't change the plan or the profit at all.

## 3. A note on the tomato "MC dip" framing

Adam's teaching example describes tomato marginal cost dipping around bed 6 as if the farmer's own hours are priced continuously at her $34.72/hr opportunity cost rather than treated as sunk — under that framing, marginal cost genuinely falls once cheaper $17.36/hr temp labor takes over past bed 5. That's not what this workbook computes: Convention A treats the farmer's first 720 hours as already paid for by her flat $25,000 labor cost, so using one more of them is free at the margin — flat $880 for beds 1–4, then a step up (not a dip) at bed 6. The two framings differ on whether her time is a sunk cost or a true per-hour opportunity cost; this model uses the former.

## 4. Why grow crops that lose money on their own

MC stayed below price at every single carrot bed (through 20) and every mesclun bed (through 30). Since average variable cost is just the average of all those per-bed marginal costs, and every one of them stays below price, AVC must stay below price too. You can't average a column of numbers that are all below a line and land above it. That's the short-run shutdown rule directly: produce as long as price covers AVC, because the fixed cost gets paid either way.

And the $20,000 really is farm-wide and singular in the Inputs, one number, not one per crop. A standalone P&L that charges the full $20,000 against carrots alone is asking one crop to carry all the weight. Once carrots and mesclun are grown together with tomatoes, that $20,000 is being paid regardless of the planting decision, so it's irrelevant to whether one more bed of carrots is worth planting. The only question that bed answers is "does its own price beat its own marginal cost," and for every carrot and mesclun bed up to the cap, then yes. It's the same reasoning as the half-empty airline route: the plane and crew are sunk cost for the flight either way, so any fare above the cost of that one extra passenger's fuel and meal is pure profit, even though the flight "loses money" if you insist on dividing the airline full cost by the empty seats.
