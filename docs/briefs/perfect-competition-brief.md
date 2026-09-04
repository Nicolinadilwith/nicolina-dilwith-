# Perfect Competition Brief

## Problem

We need to find the most profitable combination of vegetables by taking into account the price, labor, etc. with a maximum of 64 beds.

I hypothesize that the most profitable combination of beds will be 7 beds of tomatoes, 18 beds of carrots, and 22 beds of mesclun, for a total of 47 beds. This combination should produce the highest profit because it balances the relatively high price of tomatoes with the lower labor requirements and slower diminishing returns of carrots and mesclun.
The 7 tomatoes / 18 carrots / 22 mesclun = 47 beds (17 idle) figure is the pre-analysis hypothesis — a guess made before the labor-hours engine was ever run.

The model's actual recommendation, in analysis/figures/Nicolina-Perfect Competition Memo and Reflection.docx, is 10 tomatoes / 19 carrots / 28 mesclun = 57 of 64 beds (only 7 idle), profit $16,586. 

Why the hypothesis's 17 idle beds don't hold up:

Recomputing the hypothesis's own numbers: at 7/18/22, the farm uses 3,371 labor-hours against 3,600 available from the farmer + 2 temp workers she'd already need to hire — 229 hours of slack, and nowhere near a point where any crop's next bed costs more than it earns (we know that because the model shows 10 more beds were worth planting). The reflection says: this guess was too conservative on every crop, leaving $11,334 on the table. It wasn't derived from either mechanism — it was an intuitive guess that turned out to undershoot.

Why the real answer — 7 idle beds at 57/64 — does hold up:

Tomatoes stop at 10 (cap is 20). Bed 11's own marginal cost is $9,391 ($8,511 in labor + $880 fertilizer) against an $8,800 price — a straightforward loss, even pricing labor smoothly and continuously. Diminishing returns catches up with tomatoes specifically because their HRS_PER_BED (2.5) and DIM_PCT (10%/bed) are both far higher than the other two crops.

Carrots stop at 19 (cap 20) and mesclun at 28 (cap 30) — and neither fails that same test. Priced the same smooth way, carrot bed 20 would earn about +$406 at the margin and mesclun bed 29 about +$313. In isolation, both crops still want to keep growing. 

At 10/19/28 the farm has already used 5,029 of the 5,040 hours available from the farmer plus 3 temp workers (720 + 3×1,440) — 10 hours of slack. Add any single one of those next beds and total hours cross 5,040, which doesn't cost you $17-ish more, it costs you a whole fourth worker: $25,000 for 1,440 hours, to cover a bed that earns a few hundred dollars.
