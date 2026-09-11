# Perfect Competition Brief

## Problem

We need to find the most profitable combination of vegetables by taking into account the price, labor, etc. with a maximum of 64 beds.

I hypothesize that the most profitable combination of beds will be 7 beds of tomatoes, 18 beds of carrots, and 22 beds of mesclun, for a total of 47 beds. This combination should produce the highest profit because it balances the relatively high price of tomatoes with the lower labor requirements and slower diminishing returns of carrots and mesclun.

> **AI note, added after the analysis:** this hypothesis leaves 17 of 64 beds idle, which is a strong claim — it can only hold if the farm has run out of labor at 47 beds, or if the next bed of every crop costs more to grow than it earns. Neither is true here. At 7/18/22 the farm needs about 2,651 hours of temp labor, well under the 5,760-hour cap the farm can buy (equivalent to 4 full-time temp workers) — nowhere near a binding labor limit. And the actual analysis (see `analysis/figures/Nicolina-Perfect Competition Memo and Reflection.docx`) shows the opposite of "next bed costs more than it earns": 13 more beds (3 more tomatoes, 2 more carrots, 8 more mesclun, for 60 of 64 — the full 20- and 30-bed caps on carrots and mesclun) were still profitable to add, raising profit from $34,233 to $42,762. So the 17 idle beds in this hypothesis weren't derived from either mechanism — they came from an intuitive guess made before running the labor-hours engine, and the guess undershot on every crop.
