# Marginal analysis

Capability: modeling diminishing returns to labor and finding the profit-maximizing crop mix for
a price-taking farm (perfect competition — price per bed is fixed, not set by the farm) by
comparing marginal cost to price bed by bed.

- `spec.md` — the specification of the model's engine: the labor-hours formula, the two labor-cost
  allocation conventions, the objective, and the constraints. Written in logic (named parameters
  and formulas), not cell addresses, so it stands on its own from any particular build.
- See `docs/briefs/perfect-competition-brief.md` for the scoping and hypothesis written before
  this work, and `docs/decisions/` for the recommendation once it's written up.
- The Excel build and its Solver troubleshooting log currently live at
  `capabilities/Nicolina - Farm_Profit_Analysis.xlsx` and `capabilities/spec.md` (the workbook and
  a debugging transcript — build artifacts, not the spec).
