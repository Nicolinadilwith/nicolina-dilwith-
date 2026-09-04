<!-- PR TARGET: https://github.com/Nicolinadilwith/nicolina-dilwith- | Stage 1.2 -->
# Stage 1.2 review — spec, build, audit

**Spec:** [`capabilities/perfect-competition/spec.md`](https://github.com/Nicolinadilwith/nicolina-dilwith-/blob/main/capabilities/perfect-competition/spec.md)

> Graded 2026-09-04, first pass on this stage. You have a real specification, a real six-sheet workbook that produces a coherent answer, and a written memo. None of it is where the stage looks for it, which is the only reason this is held rather than entered.

| Criterion | Where it stands |
|---|---|
| Spec completeness — inputs, structure, calculation flow | A genuine specification with the case's inputs, a stated structure and a calculation flow a builder could follow — and the workbook beside it proves that, because it was built from this. What holds it back is placement and precision: it lives at capabilities/perfect-competition/spec.md rather than capabilities/marginal-analysis/spec.md, and the costing convention is described rather than pinned down, which is why the model ends up on the cash reading without ever declaring it as a choice. |
| Spec validation rules | There are checks and the workbook has an Audit sheet driving them, which is more than half this cohort has. What is missing is the part that makes checks meaningful: no acceptance figure from the case appears as a required value, there is no hand-calculated labor anchor, and no tolerance is stated anywhere. A check without a target tests that the sheet computed something, not that it computed the right thing. |
| Workbook satisfies the contract | Six sheets — Inputs, Solver Model, Engine, Marginal Analysis, P&L and Audit — and 371 formulas. The structure is thoughtful and the separation of the engine from the presentation layers is better than most. Two things cost marks and both are contract items rather than judgement calls. There are zero named ranges in the entire workbook, so every formula addresses cells by coordinate and the specification's named contract is not actually implemented. And the file is capabilities/Nicolina - Farm_Profit_Analysis.xlsx rather than capabilities/marginal-analysis/model.xlsx — a name with spaces, at a path the stage does not look at. |
| Audit note | There is an Audit sheet in the workbook and a written memo, and the memo does the comparison honestly — it names the gap between your hypothesis and the model's answer and quantifies it at $11,334. What is missing is the audit this stage asks for: checks run against the built model, each recording what was checked, what it was intended to catch, what was found and what was done about it. The memo is a Stage 1.3 deliverable doing Stage 1.2's job. |

### The three moves that turn this into a grade

- Move the specification to capabilities/marginal-analysis/spec.md.

- Move the workbook to capabilities/marginal-analysis/model.xlsx. Rename it — no spaces, no personal name in the filename. The folder identifies whose it is.

- Delete capabilities/perfect-competition/ once both are moved, and either finish or remove capabilities/pricing-power/, which is a second capability folder with a 356-byte stub in it.

The capability is the reusable method: marginal analysis. perfect-competition is the engagement that exercised it. Those are two different things and the folder structure is meant to keep them apart. This has now been flagged in four consecutive reviews, and it is currently the difference between a held provisional and an entered score on the highest-weighted stage in the case.

### The named ranges are the other real gap

Your workbook has none. Every formula points at a coordinate.

The reason the stage asks for them is not tidiness. A formula reading =BEDS_TOMATO*PRICE_PER_BED_TOM states what it means and breaks loudly if the input moves; =B5*C7 states nothing and breaks silently. Ethel Sumibcay's audit this week found two sheets of her workbook disagreeing about whether the model was feasible, and the sheet that was right was the one referencing named ranges while the one that was wrong used typed coordinates. That is the argument in one example.

Adding them to an existing workbook is not a rebuild — select the cell, type the name in the Name Box, then find and replace the coordinate in the formulas that use it. Your Inputs sheet is where it matters most and it is about twenty cells.

### Your answer and andrea weiss's agree exactly, and it is worth knowing why

You both recommend 10 tomato / 19 carrot / 28 mesclun at a profit of $16,586, from independent specifications and independent workbooks.

It follows from a costing choice you both made: charging the farmer's full $50,000 and each temporary worker's full $25,000 as cash in whole blocks, rather than charging the hours actually used at a derived hourly rate. Under that reading 10 / 19 / 28 with three workers hired genuinely is the optimum, and the fourth worker destroys profit because $25,000 buys 1,440 hours to service beds worth a few hundred dollars at the margin. Your brief makes that argument explicitly and it is a good one.

The published figures use the other convention — hours consumed, priced at $50,000 over 1,440 and $25,000 over 1,440 — and give 10 / 20 / 30 at $42,761.66. For this stage, build to the published convention so your checks can be verified against a known answer, and keep the cash argument for the Stage 1.3 memo where it is the point rather than where it makes the model unverifiable.

---

### How to work this review

Treat this PR the way an analyst treats feedback from a senior reviewer — a review is a proposal to engage with, not a checklist to rubber-stamp.

1. **Read it yourself first.** Form your own view before you change anything. Disagreeing *with a documented reason* is a legitimate, senior response.
2. **Stress-test it with an LLM.** Paste this review and your spec into your assistant and ask it to (a) explain anything you are unsure of, and (b) argue the *other side*.
3. **Then correct the spec, not the workbook.** When a check fails, you fix the specification and regenerate, so the document keeps describing what was actually built.
4. **Close the loop.** Reply in this thread with what you changed and what you pushed back on, then commit and push.

*Your score and the per-criterion breakdown are in your Lamaku comment, not here — this repository is public.*

— Adam
