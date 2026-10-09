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

## 2026-09-25 through 2026-10-09 — Individual research paper: brief, spec, figures, draft

- **Tool:** Claude Code
- **Asked for:** work through the Ask/Plan/Draft stages of the individual research paper — a challenge in my own words, data sources checked against real pages, two figures built from specs I reviewed, and reaction to drafts I wrote myself in Word.
- **What I got:** national and local data series (APPA pet-industry growth, BLS pet-care-services output, Hawaii unemployment, mainland and Honolulu daycare pricing) pulled and organized year-by-year; two figures built from specs I wrote; a line-by-line read of my own draft that caught a fabricated-looking reference list, a continuity gap (a "retail's floor space" reference with nothing introducing it), an unsupported claim, and grammar breaks from my own edits.
- **What I checked:** every external figure against the actual source page, not the search summary alone — this is how the fake Hawaii unemployment number and the six ungrounded APPA citations got caught before they reached the spec or the paper.
- **What I did with it:** chose the challenge, wrote the brief and hypothesis, decided the recommendation and its objection myself; used the verified data and built figures in the spec and the paper; rebuilt the reference list to the real sources once the fabricated ones were caught.

### Reflection

AI was extremely helpful when it came to searching the web in one fell swoop for statistics that represent what I am trying to compare, finding numbers across years and organizing them in a way that is easy to examine. Doing that myself would have taken a lot more time and reading, and I probably would not have found statistics from reports that were published as reflections of the industry from earlier years, since those "old" reports would not be considered relevant for someone searching for the climate on this industry unless they were specifically doing a comparison or study like I am.

My original References section had six APPA "State of the industry" citations, one for each year, but each one was pointing to just the generic APPA homepage. Only two real sources actually existed behind the growth-rate numbers, and the other numbers needed to be verified by searching through the site. They looked like proper citations, but they weren't actually verified source by source.

Although using AI to find data was very efficient, everything needs to pass a "real life" logic check instead of taking it at face value. For example, an early search handed back a Hawaii unemployment figure (5.7% in December 2022) that didn't fit the rest of the series and turned out to be wrong. We caught and discarded it before it ever reached the spec.
