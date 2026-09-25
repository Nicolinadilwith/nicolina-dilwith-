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

The more relevant series — the "other services" category (grooming, boarding, dog walking,
training, pet sitting), which is the actual category my business sits in rather than the whole
pet industry lumped together:

| Year | Spending | YoY growth |
|------|---------|-----------|
| 2022 | $11.4B  | +20%       |
| 2023 | $12.3B  | +7.9%      |
| 2024 | $13.0B  | +5.7%      |
| 2025 | $14.3B  | +10.0%     |

Sources: https://todaysveterinarybusiness.com/us-pet-spending-appa-090423/ (2022) and APPA's own
2023/2025 releases (2023–2025):
https://americanpetproducts.org/news/u.s.-pet-industry-reaches-147-billion-in-sales-in-2023 ,
https://americanpetproducts.org/news/u.s.-pet-industry-reaches-158-billion-in-2025-poised-for-continued-growth-in-2026

Two open items I still need to decide, not data problems but interpretation calls:

1. The category label isn't worded identically across every year's report ("other services" vs.
   "grooming, boarding, training and other services") — I should check whether APPA changed what's
   bucketed into it before treating the four years as a clean apples-to-apples series.
2. Growth in this category ticks back up to 10% in 2025 after falling to 5.7% in 2024 — it doesn't
   decelerate as cleanly as the aggregate industry number does. I need to either explain that uptick
   or be upfront that my own business's numbers are the real evidence and this series is supporting
   context, not a perfect national mirror of my situation.

The plan: line up my own year-over-year revenue growth rate against this category's national growth
rate, year by year, to see whether my business's pattern tracks the national one (support for "this
is a broad, cohort-driven normalization, not something specific to me or my business decisions") or
diverges from it in a way that needs its own explanation.

## Figures planned

[What chart(s) you'll build, what claim each one is evidence for, and why the paper would be
weaker without it.]

## Success criteria

[What has to be true for this paper to be finished and good — stated as checkable claims, not
just "write a good paper."]
