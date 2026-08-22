# AI conventions

How AI gets used in this repository, and what doesn't get committed.

## What AI can do

- Mechanical, structural work: scaffolding folders and stub files, formatting, boilerplate, fixing syntax errors. Build it, then verify it.
- First-pass research and summarization, always checked against the source before it goes in a deliverable.
- Editing help on my own drafts — tightening language I already wrote, not writing it from scratch.

## What has to be mine, first draft included

- Briefs, analyses, decision memos, and reflections. AI can react to a draft; it doesn't write the draft.
- The bio in `README.md` and the content of `RESUME.md`. No invented biography, ever.
- Any recommendation or conclusion. AI can help me see options; the call is mine.

## Verification, every time

Before accepting AI-generated output into this repo, I check:

1. Nothing is named after a course, a term, or a week.
2. Every directory that's supposed to exist actually has a file in it (Git doesn't track empty folders).
3. Placeholder text is actually placeholder text, not AI filling in details it invented.

## What never gets committed

- API keys, tokens, credentials, `.env` files.
- Raw chat exports or full conversation dumps — `prompt-log.md` gets a summary of sessions that mattered, not a transcript.
- Client or student data that isn't mine to publish.
- Office/OS temp files (see `.gitignore`).

## Logging

Sessions where AI materially shaped a deliverable get an entry in `prompt-log.md`: what I asked for, what I checked, what changed as a result.
