Reviewed below, criterion by criterion. This is entered.

**CRITERION BY CRITERION**

* **Spec completeness — inputs, structure, calculation flow** — At the canonical path at last, and the document itself is strong: named parameters with units, the decision variables, the engine formula with a written argument for why the exponent has to be there, and a marginal-cost section that tells the reader not to assume MC rises monotonically. The costing fork is pinned now rather than described — Convention A drives the objective, Convention B is reporting only, and "do not compute a separate blended rate per crop" settles it. Carrot hours are specified as exact 5/6 with the rounding consequence stated. 4.5 held: there is no Structure section naming the sheets the workbook must have. Your README does that job; the spec is where it belongs.
* **Spec validation rules** — Your checks have targets now — a q = 1 hand anchor, the published acceptance figure, a stated tolerance of a cent. They live on the workbook's `Audit` sheet, though, not in the spec, so the contract still does not say what the build has to reproduce. A check that sits inside the thing it is meant to gate cannot gate it; if the workbook were rebuilt from the spec tomorrow, none of those targets would come with it.
* **Workbook satisfies the contract** — 27 named ranges where there were none, and the formulas address them by name — `WEEKS`, `FARMER_RATE`, `TEMP_RATE`, the per-crop families. 374 formulas across six sheets, no error cells, and all three rounding traps closed: `Inputs!D26` is `=5/6` and both wage rates are derived from salary and hours. Convention A profit is $42,761.66 and Convention B returns the identical figure, as your own spec requires; the bed-10 marginal cost and marginal profit are exact. 2 held: the committed file carries no cached values, so it opens blank for anyone who has not recalculated it, and Solver was never run — the run log is empty and the path-dependence cell reads "Pending".
* **Audit note** — Six checks on a dedicated sheet, each naming what was checked and against what — the q = 1 hand calculation against the literal arithmetic, the MC cross-check at q = 10, Solver path-dependence, constraint reconciliation, formulas-not-values with a spot list, and the acceptance figure with its tolerance. That is the right shape. 2.5 held: two of the six are unfinished — Check 2's Farm Profit Lab reference is 0 and reads "Pending", Check 3's run log is empty — and nothing records what you found and what you did about it, which is the half of an audit the stage actually asks for.

**Repo:** https://github.com/Nicolinadilwith/nicolina-dilwith-
**Spec:** `capabilities/marginal-analysis/spec.md` (9,099 B) · **Workbook:** `capabilities/marginal-analysis/model.xlsx` (22,261 B, 6 sheets, 374 formulas, 0 error cells, **27 named ranges**) · `README.md` (951 B)

**WHAT IS STILL COSTING YOU, AND IT IS ALL RECOVERABLE**

The largest deduction left is not in the workbook. It is that your validation lives in the build rather than in the contract.

Your `Audit` sheet has real checks with real targets — the q = 1 anchor at 99 hours, the acceptance figure, a stated tolerance. I recalculated the workbook and every one of them holds. That is good work. But the spec is the document someone else builds from, and yours does not tell them what the finished model has to reproduce. Hand your spec to a stranger and they can build a workbook; they cannot tell whether they built the right one.

The same logic explains the two smaller holds. Solver was never run, so the run log is empty and your own path-dependence check reads "Pending" — the check exists, it just has not been executed. And the committed `.xlsx` has no cached values, so the file opens blank for anyone who has not recalculated it. Both are minutes of work, and both are the difference between a model that is right and a model that can be shown to be right.

**WHAT I'D FIX FIRST**

* Add a validation-rules section to `spec.md` — 7 points, the biggest single block left. Move the acceptance figure, the q = 1 anchor and the ±$0.01 tolerance out of the `Audit` sheet and into the spec as requirements, with what a builder does when one fails. Then let the sheet implement them. About half an hour, and most of it is text you have already written.
* Add a Structure section to the spec naming the six sheets and what each must hold — 4.5 points. Your README already says it; move it and expand it. Fifteen minutes.
* Run Solver from two starting points, paste the run log into Check 3, and paste the Farm Profit Lab figure into Check 2 — that clears both "Pending" cells and most of the audit deduction. Ten minutes.
* Open the workbook, let it calculate, save, and commit — so it does not open blank for a reader. Two minutes, and it is the cheapest thing on this list.

**LOOKING AHEAD**

Stage 1.3 is the memo, and your cash-costing argument belongs there. Keeping it on `Solver Model` row 44 as "a defensible alternative reading" beside the published one is exactly what I asked you to do with it — you built to the convention that can be verified and kept your own reading visible rather than abandoning it. In the memo that stops being a footnote and becomes the argument, so bring the whole-worker-block reasoning with you. And carry one habit forward: write what the answer has to be before you build the thing that produces it.

---
