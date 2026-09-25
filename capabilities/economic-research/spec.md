<!-- Stage: Plan. Data sources, the model/figures you intend to build, and the success criteria
     a finished paper has to meet — written by you, not drafted by AI (see AGENTS.md).
     Replace each bracketed line below; delete this comment when the spec is done. -->

# Spec: [paper title]

## Data sources

**My own annual revenue totals, 2022–2026.** Pulled from my own business records. This is the
core evidence for whether my growth has actually plateaued, and it's the one source nobody else
can verify for me — it goes in as-is, on my own authority.

**APPA (American Pet Products Association) State of the Industry reports.** Checked against the
linked pages myself; figures confirmed accurate.

Aggregate national pet-industry spending growth by year: roughly +10.8% (2022), +7.4% (2023, to
$147B), +3.4% (2024, to $152B), +3.7% (2025, to $158B).
Source: https://americanpetproducts.org/news/the-american-pet-products-association-appa-releases-2025-state-of-the-industry-report

I considered a category-specific series ("other services": grooming, boarding, dog walking,
training, pet sitting) as a closer match to my own business. It broadly moves in the same
direction as the aggregate figure (20% → 7.9% → 5.7%, then also ticking back up in 2025), so it's
soft corroboration, not a contradiction. But I'm not using it as primary evidence — the bucket is
still too broad, lumped in with things like pet insurance that have nothing to do with daycare
demand specifically, so its growth could be driven by a completely different segment inside it.
The aggregate figure is the one I'm building the comparison on; the category series is mentioned,
not relied on.

2025's growth did tick back up slightly from 2024 (3.4% to 3.7%), which could look like the
deceleration reversing. It isn't: 2025's 3.7% is still barely a third of 2022's 10.8%. A small
uptick within an overall decline of that size doesn't undercut the deceleration story — it's
worth stating that comparison explicitly in the paper so a reviewer doesn't raise the same
objection I did before I'd worked through it.

The plan: line up my own year-over-year revenue growth rate against this aggregate national growth
rate, year by year, to see whether my business's deceleration pattern tracks the national one
(support for "this is a broad, cohort-driven normalization, not something specific to me or my
business decisions") or diverges from it in a way that needs its own explanation.

**Hawaii/Oahu unemployment rate, annual.** For the sustainability question — checking whether my
plateau lined up with a weakening local economy or happened despite a strengthening one.
Best sources: Hawaii DBEDT's own data (https://dbedt.hawaii.gov/economic/unemployment-statistics/)
and/or FRED's Honolulu County series, which is Oahu-specific rather than statewide
(https://fred.stlouisfed.org/series/LAUCN150030000000003A). Approximate figures found so far:
statewide annual average ~3.3% (2022), ~3.0% (2023), ~3.1% (2024), ~2.5% (2025) — a tightening
labor market across the whole window my growth plateaued, which argues against the plateau being
explained by a weakening economy. Checked against the linked pages myself; figures confirmed
accurate.

**Mainland high-end daycare pricing benchmark.** For the pricing/positioning question — comparing
my own day rate against what premium mainland facilities charge. New York: $40–60/day generally,
Manhattan $50–70/day (https://www.rover.com/blog/new-york-city-ny-doggy-day-care-price/). Los
Angeles: premium facilities $45–59/day
(https://www.dogdrop.co/blog/how-much-does-dog-daycare-cost). San Francisco: average $56.42/day
(https://www.rover.com/blog/san-francisco-ca-doggy-day-care-price/). Checked against the linked
pages myself; figures confirmed accurate.

## Figures planned

**Figure 1: my revenue growth rate vs. the national industry growth rate, 2022–2026.** A line
chart, year on the x-axis, year-over-year growth rate (%) on the y-axis, two lines — my own
business and the aggregate APPA national trend. Same units on both lines (growth rate, not raw
dollars) so they're actually comparable on one axis, not a dual-axis chart that just looks
comparable.

This is the load-bearing figure for the sustainability question. The claim it's evidence for:
if my line decelerates roughly the way the national line does, that supports the cohort-effect
explanation (a broad, national normalization, not something specific to my business); if my line
diverges sharply from the national one, that points to something specific to me instead, and I'd
need to say what. The paper would be much weaker without it — the comparison is the whole
argument for Question 1, and a reader needs to see the two curves side by side rather than take
my word for how closely they track.

Caption plan: state the finding, not just the axes — something like "Both series decelerate over
the same window, though my business's plateau is [sharper/gentler] than the national trend,"
filled in once the actual data is plotted.

## Success criteria

[What has to be true for this paper to be finished and good — stated as checkable claims, not
just "write a good paper."]
