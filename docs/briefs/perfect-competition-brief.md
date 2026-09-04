# Perfect Competition Brief

## Problem

We need to find the most profitable combination of vegetables by taking into account the price, labor, etc. with a maximum of 64 beds.

I hypothesize that the most profitable combination of beds will be 7 beds of tomatoes, 18 beds of carrots, and 22 beds of mesclun, for a total of 47 beds. This combination should produce the highest profit because it balances the relatively high price of tomatoes with the lower labor requirements and slower diminishing returns of carrots and mesclun.

> **AI note, added after the analysis:** this hypothesis leaves 17 of 64 beds idle, which is a strong claim — it can only hold if the farm has run out of labor at 47 beds, or if the next bed of every crop costs more to grow than it earns. Neither is true here. At 7/18/22 the farm uses about 3,371 labor-hours against 3,600 available from the farmer plus the 2 temp workers this plan already needs — roughly 229 hours of slack, nowhere near a binding labor limit. And the actual analysis (see `analysis/figures/Nicolina-Perfect Competition Memo and Reflection.docx`) shows the opposite of "next bed costs more than it earns": 10 more beds (3 more tomatoes, 1 more carrot, 6 more mesclun, for 57 of 64) were still profitable to add, raising profit from $5,252 to $16,586. So the 17 idle beds in this hypothesis weren't derived from either mechanism — they came from an intuitive guess made before running the labor-hours engine, and the guess undershot on every crop.
