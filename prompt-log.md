# Prompt log

Running record of AI sessions that materially shaped this repo or its deliverables. See `AGENTS.md` for what does and doesn't get logged here.

## 2026-08-22 — Workspace setup (Stage 0, part 2)

- **Asked for:** scaffold the portfolio repo skeleton per the portfolio-repo standard — root files, `capabilities/`, `docs/briefs/`, `docs/decisions/`, `data/`, `analysis/figures/`, `.claude/skills/`, and `.gitignore`.
- **What I gave it:** the real facts for the bio and resume myself (dog daycare business on Oahu, ~10 years training experience, goal to grow while keeping personal relationships with clients) — didn't let it invent a biography.
- **Checked:** no folders named after a course/term/week; every directory has at least one file; placeholder files read as placeholders, not fabricated content.
- **Still to do:** invite `adamwstauffer` as a collaborator (repo Settings, not something AI can do); fill in `capabilities/pricing-power/` with real work once the first engagement starts.

## 2026-08-23 — Excel Solver debugging (Farm Profit Model)

- **Tool:** Claude (web)
- **Asked for:** help getting Excel's Solver add-in to run against the farm bed-allocation model — hit a run of errors: invalid constraint syntax, the "int" constraint being typed instead of picked from the relation dropdown, Solver scoped to the wrong active sheet, "Ignore Integer Constraints" silently dropping the integer requirement, and an infeasible starting point.
- **What I got:** a step-by-step fix for each error in turn, plus direct inspection of uploaded workbook/result files to diagnose fractional bed counts, a swapped Start/Final run-log row, and confirmation that a 20/0/0 starting point was infeasible before Solver even began.
- **What I did with it:** applied each fix in Excel, corrected the run log by hand, and re-ran Solver from both starting points.

## 2026-09-04 through 2026-09-18 — Stage 1.2/1.3: labor-costing convention, workbook rebuild, analysis + memo

- **Tool:** Claude Code
- **Asked for:** reconcile the model's 10/19/28 ($16,586) answer against the case's published 10/20/30 ($42,761.66); apply the Stage 1.2 review's required moves (named ranges, file paths, folder cleanup); draft the Stage 1.3 analysis and memo section by section from my own drafts.
- **What I got:** identification of the labor-costing convention responsible for the gap (discrete $25k/$50k blocks vs. continuous per-hour pricing) and the exact input-precision fix (carrots' hours/bed) needed to match the published figure to the penny; ~27 named ranges added across the workbook; a separate bug found in the per-bed marginal-cost tables (free hours priced at $0 instead of the farmer's rate), which didn't reproduce the case's own check-yourself numbers until corrected.
- **What I did with it:** rebuilt the Solver Model/P&L/Engine/Marginal Analysis formulas to the corrected convention and fixed the free-hours bug; wrote the analysis findings and memo sections myself, with cell citations and figures added against the corrected model; moved `spec.md`/`model.xlsx` to `capabilities/marginal-analysis/` and removed the duplicate `capabilities/perfect-competition/` folder per the review.

### Reflection (Stage 1.3)

The model I first built priced temp labor in blocks. Hiring a worker meant paying the full $25,000 for their 1,440 hours whether or not all of it was used. That convention answers $16,586 in profit. The mismatch only surfaced because I asked the AI to reconcile my output against the specific published target. It took several wrong conventions before landing on the right one. Labor priced continuously by the hour, the farmer's first 720 hours "free" and every hour after billed at the temp rate, with no worker blocks. That method caught another error: carrots' hours per bed needed to be 5/6, not 0.833 I had. The difference was about $7 of profit, not noticeable by eyeballing. Both errors only came up because a specific number didn't match and had to be run down by formula.

Two more mismatches turned up the same way. First, total labor cost was off by exactly $25,000. The farmer's hours were treated as free while P&L was billing them at her $34.72/hr implied rate, so it cost off by $25,000. Second, the build didn't reproduce the case's given answers: bed 5 should cost $7,661 and bed 6 should drop to $4,906 as cheaper temp labor takes over, but the build was giving $962 at bed 5. This is a bug AI introduced and didn't catch until we went looking for why the expected dip wasn't showing up, checked against the case's published figures, and found the mismatch. The fix was pricing those first 720 hours at the farmer's $34.72/hr rate instead of $0.
