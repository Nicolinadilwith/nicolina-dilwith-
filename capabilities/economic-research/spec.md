<!-- Stage: Plan. Data sources, the model/figures you intend to build, and the success criteria
     a finished paper has to meet — written by you, not drafted by AI (see AGENTS.md).
     Replace each bracketed line below; delete this comment when the spec is done. -->

# Spec: [paper title]

## Data sources

**My own annual revenue totals, 2018–2026.** Pulled from my own business records (bookkeeping
before 2022 is less precise, but the totals are real). This is the core evidence for whether my
growth has actually plateaued, and it's the one source nobody else can verify for me — it goes in
as-is, on my own authority.

| Year | Revenue | YoY growth |
|------|---------|-----------|
| 2018 | $3,626 | — |
| 2019 | $35,835 | +888% (startup-year artifact — excluded from the comparison, see below) |
| 2020 | $35,550 | −0.8% |
| 2021 | $43,923 | +23.6% |
| 2022 | $217,358.95 | +395% |
| 2023 | $426,115.26 | +96.0% |
| 2024 | $523,755.33 | +22.9% |
| 2025 | $566,460.70 | +8.2% |
| 2026 (through Sept 1) | $373,720.36 | not projected — see note below |

2018 was a near-zero soft-launch base, so 2019's +888% is a base-effect artifact, not a real
signal — I'm using 2019 as the first "mature" baseline year and excluding the 2018→2019 growth
rate from the comparison chart (it would also wreck the chart's scale).

2026 is a partial year (through Sept 1) and I'm not projecting a full-year number. Straight-line
annualizing would say roughly flat vs. 2025, but my business is seasonal — holidays (Nov–Dec) are
my strongest months, and they're not in this partial figure yet, while the missing-period
slowdown (late Aug/early Jan, as school starts back) partly overlaps with what *is* in it. A naive
projection would understate the real number, so the paper will show 2026 as a labeled partial
point and say in the text that the full year is expected to land higher than a straight-line
estimate, not state a specific projected figure.

I confirmed directly that the 2024–2025 slowdown was demand cooling off, not me hitting physical
capacity — so this series is actually testing a demand question, not confounded by being sold out.

**APPA (American Pet Products Association) State of the Industry reports.** Checked against the
linked pages myself; figures confirmed accurate.

| Year | Total industry | YoY growth |
|------|----------------|-----------|
| 2019 | $97.1B | — |
| 2020 | $103.6B | +6.7% |
| 2021 | $123.6B | +19.3% (computed from the totals; a "13.5%" figure found elsewhere didn't reconcile with the dollar totals, so it's discarded) |
| 2022 | ~$136.8B | +10.8% |
| 2023 | $147B | +7.4% |
| 2024 | $152B | +3.4% |
| 2025 | $158B | +3.7% |

Sources: https://www.supermarketnews.com/consumer-trends/pet-industry-sales-in-2020-surpass-100-billion-for-first-time
(2019–2021) and
https://americanpetproducts.org/news/the-american-pet-products-association-appa-releases-2025-state-of-the-industry-report
(2022–2025).

**The timing lag is itself a finding, not just a data point to plot.** The national series peaks
in 2021 (+19.3%) — that's pet food, supplies, and vet care, driven by people acquiring pets while
stuck at home. My business troughs in 2020 instead (−0.8%), because daycare is the opposite kind
of good: nobody needs it while everyone's already home. My boom doesn't hit until 2022–2023, a
full year after the national peak, because it depends on people *leaving* the house again and
discovering their lockdown dogs can't handle it. I need to say this explicitly in the paper —
the two series aren't supposed to move together point-for-point; the lag between them is
evidence for the mechanism, not a mismatch to explain away.

**BLS "pet care services" output data (NAICS 812910 — boarding, grooming, training, sitting; no
pet food/products, no veterinary).** Output fell **15.6% from 2019 to 2020**, a real decline in
the services segment specifically — unlike the APPA aggregate's +6.7% that same year, which is
inflated by pet food/product spending as people acquired pets while stuck at home. This is a
much closer match to my own business's −0.8% in 2020 than the aggregate is.
Source: https://www.bls.gov/opub/btn/volume-13/a-tail-of-productivity-in-pet-care-services-new-technology-enables-rapid-growth.htm

I'm **not** splicing this into the Figure 1 line alongside the APPA series — they measure
different things (BLS is services-specific output, APPA is total industry dollars including
products), so mixing them into one continuous series would mix metrics mid-stream without
saying so. Instead: Figure 1's plotted line stays the consistent APPA series throughout, and I'll
add a callout at the 2020 point citing this BLS figure as context, plus state it explicitly in
the written analysis — the paper gets the better-matched number without pretending it's part of
the same series.

**Grand View Research, "U.S. Pet Daycare Market (2025–2030)."** The narrowest category found —
scoped to pet daycare specifically, not bundled with grooming or the whole pet industry. Cited
for the mechanism, not a data series (the full year-by-year history is in the paid report, not
the free sample I read): it states "Day boarding represented over 60% share of the U.S. Pet
Daycare market by Service Type in 2024. The key factors contributing to this growth include pet
parents returning to office post-COVID..." — a third-party market research firm independently
naming the exact mechanism (return-to-office driving daycare demand) that I describe in my own
brief. Also has 2024 ($1.73B) and 2025 ($1.87B, ~+8.1%) market-size figures as a minor secondary
data point. Source: https://www.grandviewresearch.com/industry-analysis/us-pet-daycare-market-report

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
rate, 2019–2026, to show the full before/during/after story — my 2020 trough against the
national's 2020 rise, my 2022–2023 boom against the national's already-fading one, and both
decelerating by 2024–2025 — rather than diverging from it in a way that needs its own explanation.

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
Manhattan $50–70/day, midpoint $60 (https://www.rover.com/blog/new-york-city-ny-doggy-day-care-price/).
Los Angeles: premium facilities $45–59/day, midpoint $52
(https://www.dogdrop.co/blog/how-much-does-dog-daycare-cost). San Francisco: average $56.42/day
(https://www.rover.com/blog/san-francisco-ca-doggy-day-care-price/). Checked against the linked
pages myself; figures confirmed accurate.

**My own current day rate: $75.** My own authority, no external source needed.

**Honolulu general-market day rate.** $30–45/day, midpoint ~$37.50, confirmed by specific local
facilities (Ohana Doggie Daycare $45 full day, Pets in the City Hawaii $39.95, Family and MWR Pet
Kennels $35–45). Source: https://www.rover.com/blog/honolulu-hi-dog-daycare-price/. Checked
against the linked page myself; figures confirmed accurate.

**The finding changed once the real numbers were in, and the paper needs to say so.** The brief's
hypothesis assumed Hawaii lags mainland "bougie" pricing. My own rate ($75) is actually *above*
every mainland premium benchmark ($52–60), not below it — and roughly double the Honolulu general
average ($37.50). The real story isn't "Hawaii hasn't caught up to mainland premium pricing" —
it's that Hawaii barely has a premium tier at all. Mainland cities have enough demand for premium
care to support a deep field of competing high-end operators, which holds their prices in a
$52–60 band through competition. Hawaii doesn't have that depth of competition at the top, so my
price isn't held down the same way. This resolves the open tension from the "Link to course
economics" section: **market structure (barriers to entry/scarcity) wins over tastes and
preferences at the premium end** — the "lower cultural priority" story still explains why so few
Hawaii operators build toward premium at all, but it doesn't explain my own price, which the
scarcity/barriers-to-entry story does.

## Figures planned

**Figure 1: my revenue growth rate vs. the national industry growth rate, 2019–2026 — built.**
Saved to `figures/figure1-revenue-vs-national.png`. A line chart, year on the x-axis (2019 through
the 2026 partial point, labeled as such), year-over-year
growth rate (%) on the y-axis, two lines — my own business and the aggregate APPA national trend.
Same units on both lines (growth rate, not raw dollars) so they're actually comparable on one
axis, not a dual-axis chart that just looks comparable. 2018→2019 growth is excluded (startup-year
base effect, would wreck the chart's scale); 2019 is the first plotted baseline year instead.

This is the load-bearing figure for the sustainability question, and now it does more than one
job. It shows the lag mechanism directly — the national line rising and peaking in 2020–2021
while mine troughs, then mine exploding in 2022–2023 a year after the national peak — which is
visual evidence for *why* the two series shouldn't move together point-for-point. And it shows
both lines decelerating by 2024–2025, which is the actual evidence for the cohort-effect
explanation (a broad normalization, not something specific to my business). The paper would be
much weaker without it — a reader needs to see both the lag and the shared deceleration, not take
my word for either.

Caption plan: state both findings, not just the axes — something like "My business troughs in
2020 and peaks a year after the national trend, consistent with daycare demand depending on
people returning to normal activity rather than pet acquisition itself; both series decelerate
by 2024–2025," plus a footnote at the 2020 point citing BLS's −15.6% pet-care-services figure as
context for why the aggregate line actually understates how hard services specifically were hit
that year.

**Figure 2: my day rate vs. Honolulu average and mainland premium benchmarks — built.** A bar
chart, five bars in ascending order: Honolulu average ($37.50), LA premium ($52), SF premium
($56.42), NYC premium ($60), my own rate ($75, highlighted in a distinct color from the other
four, which are de-emphasized since they're context, not the subject). Saved to
`figures/figure2-pricing-comparison.png`.

This is the evidence for the pricing/positioning question, and it reversed what the brief
assumed: instead of showing a gap *below* mainland pricing, it shows my rate sitting *above*
every benchmark, roughly double the Honolulu average. That's the direct visual evidence for the
market-structure-wins finding above — a reader sees the three-tier picture (local average, deep
mainland premium competition, me alone at the top) in one chart rather than taking my word for
why my price doesn't fit the brief's original assumption.

Caption (as built): "Honolulu's general market averages $30–45/day; mainland premium facilities
(LA, SF, NYC) run $52–60/day; my own day rate is $75 — roughly double the Honolulu average and
above even mainland premium pricing. With almost no local competition at the premium tier,
there's little pulling my price back down toward either band."

## Success criteria

[What has to be true for this paper to be finished and good — stated as checkable claims, not
just "write a good paper."]
