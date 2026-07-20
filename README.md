# 70 Claude Cowork Prompts (Tested, Copy-Paste Ready)

A library of 70 prompts for **Claude Cowork** — Anthropic's agentic desktop app that works directly in your files and folders. Every prompt here is *Cowork-native*: it reads real files, produces real output files, and would be pointless in a plain chat window. Each one follows the same 5-part frame — inputs, task, output, standards, guardrails — explained in [**The Anatomy of a Good Cowork Prompt**](anatomy.md).

**How to use:** find your task below → copy the prompt → swap the file paths for your own → run it in Cowork. The *why it works* line under each prompt tells you which part is doing the heavy lifting when you adapt it.

## Categories

| # | Category | Prompts |
|---|---|---|
| 01–10 | [Documents & Reports](prompts/documents-reports.md) | KPI reports, monthly reports, digests, close packages |
| 11–20 | [Spreadsheets & Data](prompts/spreadsheets-data.md) | Reconciliation, CSV cleanup, merges, change reports |
| 21–30 | [Presentations & Decks](prompts/presentations.md) | Deck refresh, QBR decks, audits, speaker notes |
| 31–40 | [Research & Summarization](prompts/research-summarization.md) | Competitive briefs, cited memos, parallel research |
| 41–50 | [Email & Communication](prompts/email-communication.md) | Follow-ups, digests, announcements, inbox triage |
| 51–60 | [Project Management](prompts/project-management.md) | Action trackers, status snapshots, risk logs |
| 61–70 | [Team Workflows & Knowledge](prompts/team-workflows.md) | Onboarding, context folders, glossaries, playbooks |

About half of these prompts are single-run versions of the [**25 Claude Cowork team workflows**](https://github.com/claude-cowork-training/claude-cowork-team-workflows) — those link to their parent workflow, which adds the one-time setup, cadence, and failure fixes for running it as a recurring team system. New to Cowork entirely? Start with the [free 10-lesson interactive course](https://github.com/claude-cowork-training/cowork-course).

All 70 prompts are below, in full. ⭐ Star the repo to find it again — new prompts are added monthly (see [CHANGELOG.md](CHANGELOG.md)).

---
## Documents & Reports — Claude Cowork Prompts

Prompts for drafting, updating, and assembling business documents and reports — KPI summaries, monthly reports, status digests, close packages, and variance commentary — directly from the files in your folders.

---

### 01. Write a weekly KPI report from a metrics CSV and last week's report

```
Read kpi/metrics.csv and the most recent report in kpi/reports/.
Produce this week's KPI report in exactly the same structure as
the most recent one:
- Headline first: the single most important change this week.
- A table of every metric with this week's value and the delta
  vs last week.
- One line of explanation for any metric that moved more than
  10%. If the cause isn't in the data, write "cause unknown —
  needs input" instead of guessing.
Save as kpi/reports/kpi-report-YYYY-MM-DD.md using today's date.
If metrics.csv is missing this week's row, stop and tell me
instead of reusing last week's numbers.
```

*Why it works:* Last week's report is the template — structure drift disappears when the format anchor lives in the same folder as the data.
*Part of the [01. Weekly KPI Report](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/reporting/01-weekly-kpi-report.md) workflow.*

### 02. Draft a monthly business report from metrics, notes, and last month's example

```
Read monthly/monthly-metrics.csv, the most recent report in
monthly/reports/, and monthly/notes.md.
Write this month's report, one page, identical structure to
last month's:
- Headline first (the one sentence leadership should remember).
- The key numbers in a table with month-over-month deltas.
- "What drove it" — every surprising number gets a one-line
  cause taken from notes.md; if notes.md doesn't explain it,
  write "needs explanation from owner".
- Risks & opportunities — mandatory even in a good month.
Output as .docx: monthly/reports/monthly-report-YYYY-MM.docx.
Don't invent causes the notes don't support.
```

*Why it works:* Separating numbers (CSV) from narrative (notes.md) means every "why" in the draft is traceable to a human, not a guess.
*Part of the [03. Monthly Business Report](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/reporting/03-monthly-business-report.md) workflow.*

### 03. Build a weekly client status digest from a folder of meeting notes

```
Read everything in digest/weekly-inputs/ (this week's meeting
notes and the pipeline CSV) and the example in digest/examples/.
Write this week's client status digest in exactly the example's
format: one section per active client, max 5 lines each, with
status (GREEN/YELLOW/RED), a one-line why, and next action +
owner + date.
A RED status must include a named recovery action.
End with a "Needs a decision" list — include it even if empty.
Statuses come from evidence in the notes, not optimism: if the
notes don't support GREEN, it isn't GREEN.
Save as digest/client-digest-YYYY-MM-DD.md.
```

*Why it works:* The "evidence, not optimism" rule stops status inflation — the most common failure when notes are sparse.
*Part of the [04. Weekly Client Status Digest](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/reporting/04-weekly-client-status-digest.md) workflow.*

### 04. Assemble a monthly close report from a folder of finance exports

```
Read every file in this month's close folder (close/YYYY-MM/ —
use the current month) and last month's report in close/reports/.
Assemble this month's close report in the identical structure:
1. Summary figures with MoM deltas, each traced to its source
   export (cite file + row/section).
2. Notable items — anything >10% off prior month, with the
   explanation from close-notes.md; if the notes don't explain
   it, flag "[EXPLAIN: ...]" for the controller.
3. Open items — anything the exports show as unreconciled.
Never net, adjust, or reclassify figures — report them exactly
as exported and flag inconsistencies instead.
Output as .docx: close/reports/close-report-YYYY-MM.docx.
If an expected export is missing, stop and list what's missing.
```

*Why it works:* The never-adjust rule converts helpful "corrections" into flagged discrepancies — in a close package, the discrepancy IS the finding.
*Part of the [16. Monthly Close Report Assembly](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/finance/16-monthly-close-report-assembly.md) workflow.*

### 05. Draft variance commentary comparing actuals to budget spreadsheets

```
Read variance/actuals-YYYY-MM.csv, variance/budget-YYYY.csv,
variance/context-notes.md, and last month's commentary in
variance/reports/.
Materiality: variances over 10% AND over $2,000.
Produce this month's commentary in the same format:
1. Variance table: line item, actual, budget, variance $ and %,
   material yes/no.
2. For each material variance, a one-paragraph draft explanation
   — ONLY from context-notes.md or clear patterns in the data.
   Anything else gets "[JUDGMENT: likely candidates are X or Y —
   finance to confirm]".
Never write a confident explanation you cannot source. Label any
forward-looking statement as an expectation, not a fact.
Save as variance/reports/variance-YYYY-MM.md.
```

*Why it works:* The source-or-flag rule isolates the real finance work into visible [JUDGMENT] flags instead of plausible-sounding invented causes.
*Part of the [20. Variance Commentary Draft](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/finance/20-variance-commentary-draft.md) workflow.*

### 06. Update an existing report with this month's numbers without touching the prose

```
Read reports/quarterly-review.docx and the new figures in
data/latest-metrics.csv.
Update the report:
1. Replace every figure that has a newer value in the CSV; keep
   all surrounding prose, formatting, and section order intact.
2. List every replacement you made (old value → new value +
   CSV row) at the end of your reply.
Save the result as a new file, reports/quarterly-review-updated
.docx — never overwrite the original.
If a figure in the report has no matching row in the CSV, leave
it unchanged and flag it as [NO SOURCE] in your list rather
than deleting or estimating it.
```

*Why it works:* Save-as-new plus a replacement log makes every change reviewable — the original stays untouched as the fallback.

### 07. Turn a folder of meeting notes into a project status report

```
Read every file in meeting-notes/ from the last two weeks and
the project plan in planning/project-plan.md.
Draft a status report with four sections: Done, In progress,
Blocked, and Decisions needed.
- Every item cites the note file it came from.
- "Blocked" items name what they're waiting on and who owns it.
- Compare progress against the milestones in the plan; call out
  any milestone the notes suggest will slip.
Output as drafts/status-report-YYYY-MM-DD.md.
Keep it under one page. Don't infer completion — if the notes
don't say a task is done, it goes in "In progress". If the
notes contradict each other, flag it with [CHECK: ...].
```

*Why it works:* Citing the source note per item makes a synthesized report auditable in seconds instead of re-reading the whole folder.

### 08. Condense a long report into a one-page executive brief

```
Read reports/annual-operations-review.docx (about 40 pages)
and the format example in reports/examples/exec-brief.md.
Write a one-page executive brief in the example's structure:
- Three headline findings, one sentence each.
- A short table of the five most decision-relevant numbers,
  each with the page or section it came from.
- Recommended actions, taken only from the report's own
  recommendations section — do not add your own.
Save as drafts/exec-brief-YYYY-MM-DD.md.
Every claim must be traceable to the source report; if two
sections of the report disagree, flag it with [CONFLICT: ...]
instead of choosing a side.
```

*Why it works:* Restricting recommendations to the report's own keeps the brief a faithful compression, not a new opinion the author never signed.

### 09. Draft a client proposal by reusing sections from past winning proposals

```
Read the client brief in clients/new-client/brief.md and the
three past proposals in proposals/examples/.
Draft a proposal for this client:
1. Follow the section structure the example proposals share.
2. Reuse boilerplate sections (approach, process, terms) from
   the examples, adapted to this client's brief.
3. Write the scope and deliverables sections fresh from the
   brief — mark anything the brief leaves ambiguous with
   [CLARIFY WITH CLIENT: ...].
Output as .docx: proposals/drafts/new-client-proposal.docx.
Leave pricing as a [PRICING — TO BE FILLED] placeholder; never
carry over prices, client names, or project specifics from the
example proposals.
```

*Why it works:* The no-carryover guardrail prevents the classic reuse accident — another client's name or price surviving into the new draft.

### 10. Standardize a folder of mixed-format documents against a house template

```
Read every document in docs/policies/ and the house template
in templates/policy-template.md.
For each policy document, produce a version restructured to the
template's sections (Purpose, Scope, Policy, Exceptions, Owner,
Last reviewed) — keep the original wording wherever it fits;
only move and label, don't rewrite meaning.
Save each as docs/policies/standardized/<original-name>.md,
leaving the originals untouched.
If a document is missing content for a required section, insert
"[MISSING: section owner to complete]" rather than drafting the
content yourself. End with a summary table: file, sections
filled, sections missing.
```

*Why it works:* "Move and label, don't rewrite" scopes the job to structure — the content owners keep authorship, and the gaps become an explicit to-do list.

## Spreadsheets & Data — Claude Cowork Prompts

Prompts for cleaning, deduplicating, reconciling, and summarizing CSV files and spreadsheet exports — messy data in, reviewable files out.

---

### 11. Match Two Exports and Produce an Exception Report

```
Read data/recon/file-a.csv and data/recon/file-b.csv.
Match line items on exact amount plus a date within 3 days.
Produce data/recon/exceptions.md with four sections:
1. MATCHED — count and total value only.
2. NEAR MATCHES — pairs matching on amount but not date (or vice
   versa), shown side by side with what differs.
3. UNMATCHED IN A / UNMATCHED IN B — full rows.
4. DATA PROBLEMS — malformed rows, duplicate references,
   inconsistent date formats.
Apply the rules mechanically — never decide a near match
"probably" matches; every judgment call stays in NEAR MATCHES.
Do not modify either source file.
```

*Why it works:* The match rule is stated explicitly and judgment is banned, so every discrepancy lands in a list a human reviews instead of being silently "resolved".
*Part of the [17. Reconciliation Prep](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/finance/17-reconciliation-prep.md) workflow.*

### 12. Clean a Raw Expense CSV and Build a Missing-Items Chase List

```
Read finance/expenses/expenses-raw.csv.
Produce two files:
1. finance/expenses/expenses-clean.csv — dates normalized to
   YYYY-MM-DD, amounts as plain numbers, rows sorted by person
   then date. Never delete or merge rows; anything unfixable
   passes through unchanged with a "FLAG" column noting why.
2. finance/expenses/chase-list.md — grouped by person: rows with
   missing notes, missing categories, or unreadable amounts,
   plus a total per person.
Do not infer a category or amount from a vague note — flag it.
Leave the raw CSV untouched.
```

*Why it works:* Splitting the output into a clean file and a chase list separates what's fixable mechanically from what needs a human answer.
*Part of the [18. Expense Report Cleanup](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/finance/18-expense-report-cleanup.md) workflow.*

### 13. Turn a Pipeline CSV into a Meeting-Ready Stale-Leads Summary

```
Read sales/pipeline.csv (columns: lead, source, stage, est_value,
owner, last_touch). Today is [DATE].
Produce sales/pipeline-review.md with:
1. Total pipeline value, and value by stage.
2. A stale table: every lead with last_touch more than 10 days
   ago — lead, owner, days since touch, est. value.
3. One recommended action per stale lead based on its stage,
   phrased as a suggestion, not a verdict.
Keep the whole file under one page; tables over prose.
If any row has a missing owner or last_touch, list it under
"data problems" instead of skipping it silently.
Do not edit pipeline.csv.
```

*Why it works:* The date anchor plus an explicit staleness threshold makes the math checkable, and the data-problems section catches the rows that would otherwise vanish.
*Part of the [05. Pipeline Review Summary](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/reporting/05-pipeline-review-summary.md) workflow.*

### 14. Build an Invoice Aging Table from a Folder of Invoices

```
Read every file in finance/invoices/sent/ and the payment log in
finance/invoices/payments.csv. Today is [DATE].
Produce finance/invoices/aging.md with:
1. Outstanding invoices table: number, client, amount, issue
   date, terms, days outstanding, status (current / overdue).
2. Aging summary: current, 1–30, 31–60, 60+ days.
Every amount must come from an invoice file — cite the filename
per row. If an invoice's terms or issue date can't be read from
the file, list it under "unreadable — check manually" rather
than assuming net 30. Do not draft or send any client messages,
and do not modify the invoice files.
```

*Why it works:* Per-row source citations and the "unreadable" bucket stop the classic failure — a guessed due date turning into a wrongly-timed chase.
*Part of the [19. Invoice Tracker & Chase List](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/finance/19-invoice-tracker-chase-list.md) workflow.*

### 15. Summarize Multi-Channel Campaign CSVs into One Performance Table

```
Read every CSV in marketing/exports/ (one export per channel)
and the previous report in marketing/reports/.
Produce marketing/reports/campaign-summary.md with:
1. Summary table: per channel — spend, primary result metric,
   cost per result, delta vs the previous report.
2. "What moved" — one line per change over 15%; if the export
   doesn't show a cause, write "cause not in data".
Match the section structure of the previous report. Every number
must trace to an export file — note the source file per row.
If a channel's export is missing, list it as "no data received"
rather than repeating the previous period's figures.
Do not modify anything in marketing/exports/.
```

*Why it works:* Requiring a source file per number and banning carried-forward figures keeps a multi-source rollup honest when one export is late.
*Part of the [11. Campaign Performance Report](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/marketing/11-campaign-performance-report.md) workflow.*

### 16. Deduplicate a Contact CSV Without Losing Any Data

```
Read data/contacts.csv.
Find duplicate contacts: exact email matches, plus rows where
name and company match but the email differs.
Produce two files:
1. data/contacts-deduped.csv — exact duplicates collapsed to one
   row, keeping the most complete version of each field.
2. data/dedupe-review.md — the name+company near-duplicates as
   side-by-side pairs for a human decision, plus a count of
   exact duplicates removed and which rows they were.
Never merge near-duplicates yourself — a shared name and company
can be two people. Never modify contacts.csv, and never fill a
blank field with a guessed value.
```

*Why it works:* Splitting exact duplicates (safe to collapse) from near-duplicates (human call) is the line that makes automated deduping trustworthy.

### 17. Merge Monthly CSV Exports into One Master File

```
Read every CSV in exports/monthly/ — same report exported each
month, but column order and header spelling may drift between
files.
Produce exports/master.csv:
1. Map each file's columns to one canonical header set; list the
   mapping you used per file at the top of exports/merge-log.md.
2. Stack all rows, adding a source_file column and normalizing
   dates to YYYY-MM-DD.
3. In merge-log.md, list any column you could not confidently
   map and any file whose row count looks anomalous vs the
   others — do not drop or rename them silently.
Do not modify or delete anything in exports/monthly/. If two
files cover the same month, flag it in the log; don't pick one.
```

*Why it works:* The merge log makes every mapping decision visible, so header drift becomes a reviewable list instead of silently misaligned columns.

### 18. Normalize Mixed Date Formats Across a Spreadsheet Export

```
Read data/orders.csv, which mixes date formats in the same
columns (2026-06-01, 06/01/2026, "Jun 1 2026").
Produce data/orders-normalized.csv with every date as
YYYY-MM-DD, and data/date-fixes.md listing:
1. Each format found and how many rows used it.
2. Every ambiguous date (e.g., 04/05/2026 — is that April 5 or
   May 4?) with its row number, left UNCHANGED in the output
   and marked in a "FLAG" column.
Assume nothing about day/month order for ambiguous values —
flagging is the job, guessing is the failure. All non-date
columns pass through byte-for-byte. Do not modify orders.csv.
```

*Why it works:* It names the exact trap — ambiguous day/month order — and makes leaving those values alone an explicit instruction rather than hoping.

### 19. Pivot-Style Summary of a Transactions CSV by Category and Month

```
Read finance/transactions.csv (columns include date, category,
amount).
Produce finance/summary-by-category.md with:
1. A table: rows = categories, columns = months, cells = total
   amount, plus row and column totals.
2. Top 5 largest single transactions with date and category.
3. A "check these" list: rows with a blank category, a
   non-numeric amount, or an unparseable date — with row
   numbers. Include them nowhere in the totals, and say how
   many rows were excluded.
Show amounts to 2 decimals; state the grand total and confirm
it equals the sum of included rows. Do not edit the source CSV
or invent a category for blank rows.
```

*Why it works:* The self-check (grand total must equal the sum of included rows) plus an explicit exclusion count makes the summary auditable at a glance.

### 20. Compare Two Versions of a Spreadsheet and Report What Changed

```
Read data/budget-v1.csv and data/budget-v2.csv — two versions of
the same sheet, keyed by the "line_item" column.
Produce data/budget-diff.md with:
1. CHANGED — rows present in both where any value differs:
   line item, column, old value, new value.
2. ADDED — rows only in v2. REMOVED — rows only in v1.
3. A one-line net effect on the total budget column.
Sort each section by the size of the change. Report only —
never write a "fixed" or merged version, and never label a
change as an error; if two rows share a line_item key in one
file, list them under "duplicate keys — check manually".
```

*Why it works:* Diffing on a stated key column and forbidding a merged output keeps the run purely observational — you decide what the changes mean.

## Presentations & Decks — Claude Cowork Prompts

Prompts for building, refreshing, condensing, and auditing slide decks straight from the reports, metrics files, and project folders you already have.

---

### 21. Refresh Last Period's Board Deck with This Period's Numbers

```
Read the most recent deck in board/, board/metrics.csv, and
board/notes.md.
Create this period's deck: identical slide structure and order,
every figure updated from metrics.csv, and the points in notes.md
worked into the relevant slides as speaker notes.
Flag any slide where the new numbers change the story (e.g., a
trend reverses) by adding "[REVIEW]" to its title.
Save as board/board-deck-YYYY-MM.pptx — never overwrite the
original deck.
Do not add, remove, or redesign slides. If a figure in the old
deck has no matching source in metrics.csv, mark it "[SOURCE?]"
rather than carrying it forward.
```

*Why it works:* The `[SOURCE?]` rule turns the classic silent failure — stale hand-typed numbers carried forward — into a visible flag you review before presenting.
*Part of the [02. Board Deck Refresh](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/reporting/02-board-deck-refresh.md) workflow.*

### 22. Build a Client QBR Deck from the Quarter's Folder

```
Read everything in clients/acme/ for this quarter, plus the past
QBR deck in clients/acme/qbr/ as the structure anchor.
Build this quarter's QBR deck in the same structure:
1. Engagement summary — scope, term, owner.
2. What we delivered — concrete items from the notes only.
3. Outcomes — every figure cites its source file in the speaker
   notes; client-stated outcomes are labeled "client-reported,
   not independently measured".
4. What's next — open items and the coming quarter.
Save as clients/acme/qbr/qbr-YYYY-QN.pptx.
Anything you can't source gets "[NEEDS INPUT]", never a guess,
and never a number inferred from partial data.
```

*Why it works:* The "client-reported" label and per-figure citations stop casual remarks in status notes from becoming hard ROI claims on a slide.
*Part of the [10. QBR Deck Builder](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/10-qbr-deck-builder.md) workflow.*

### 23. Turn an Engagement Folder into a Case Study Deck

```
Read everything in clients/acme/ (scope, delivery notes, outcome
data) and the example deck in marketing/case-studies/example.pptx.
Draft a case-study deck in the example's structure:
1. The problem — in the client's terms, from scope and kickoff
   notes.
2. What we did — concrete and chronological, no methodology
   padding.
3. Results — ONLY figures present in the folder; every number
   cites its source file in the speaker notes.
Add "[QUOTE: ask about X]" placeholder slides where a client
voice would land. Flag every gap as "[INTERVIEW: ...]" — do not
fill gaps with plausible details.
Save as marketing/case-studies/drafts/acme-case-study-v1.pptx.
```

*Why it works:* Invented "texture" is what clients catch at approval time — the no-plausible-details rule replaces filler with an interview agenda.
*Part of the [15. Case Study First Draft](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/marketing/15-case-study-first-draft.md) workflow.*

### 24. Audit a Deck for Numbers with No Source File

```
Read decks/board-deck-current.pptx and every data file in
data/ (CSVs and spreadsheets).
For every number on every slide, find its source:
1. If it matches a value in data/, record file and row/cell.
2. If it's close but not equal, mark it "STALE" with both values.
3. If it appears nowhere in data/, mark it "ORPHAN".
Output as decks/deck-number-audit.md: one table per slide with
columns Number | Slide location | Status | Source.
Be exact — treat rounded figures as STALE, not matched, and say
so in the row.
Read-only run: do not modify the deck or any file in data/.
If data/ is empty or unreadable, stop and report that instead.
```

*Why it works:* Separating STALE from ORPHAN tells you which numbers need a refresh and which need a conversation about where they came from.
*Part of the [02. Board Deck Refresh](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/reporting/02-board-deck-refresh.md) workflow.*

### 25. Turn a Written Report into a Slide Deck

```
Read reports/q2-summary.docx and the deck template in
decks/templates/standard-deck.pptx.
Convert the report into a deck:
1. One slide per major report section, in the report's order.
2. Each slide: a headline that states the section's conclusion
   (not its topic), max 4 bullets, max 12 words per bullet.
3. Move all supporting detail into that slide's speaker notes.
4. Every number on a slide must appear verbatim in the report.
Save as decks/q2-summary-deck.pptx.
Match the section naming of the template deck.
Do not modify the source report. If a section is too thin for a
slide, merge it into its neighbor and note the merge in the
speaker notes rather than padding it.
```

*Why it works:* "Headline states the conclusion" plus hard bullet limits is what keeps a converted report from becoming paragraphs pasted onto slides.

### 26. Generate Speaker Notes for Every Slide in a Deck

```
Read decks/sales-pitch.pptx and the background material in
docs/product-overview.md and docs/faq.md.
For each slide, write speaker notes:
1. A 2–3 sentence spoken narrative that connects this slide to
   the previous one.
2. One likely audience question and a one-line answer, drawn
   from the FAQ where possible.
3. A "[VERIFY]" tag on any claim you could not confirm in the
   background docs.
Save as a new file decks/sales-pitch-with-notes.pptx — leave
the original deck untouched.
Keep each slide's notes under 120 words; write for speaking,
not reading. Do not change any slide content, only the notes.
```

*Why it works:* Tying every answer back to named background docs keeps the notes grounded in your material instead of generic talk-track filler.

### 27. Deck Consistency Audit Before It Ships

```
Read decks/client-proposal.pptx and team-context/glossary.md.
Audit the deck for internal consistency:
1. Terminology — the same product, team, or metric named two
   different ways; check names against glossary.md.
2. Numbers — the same figure appearing with different values on
   different slides.
3. Dates and periods — mixed "Q2" / "April–June" / fiscal-year
   labels.
4. Claims — slides that contradict each other.
Output as decks/proposal-consistency-report.md, ordered by
severity, each finding citing both slide numbers involved.
Report only; do not edit the deck. If two values conflict, do
not judge which is correct — list both and flag the pair.
```

*Why it works:* Asking for both slide numbers per finding makes every issue directly checkable, so the report is a fix list rather than an opinion.

### 28. Condense a 30-Slide Deck into a 10-Slide Executive Version

```
Read decks/full-project-review.pptx (about 30 slides).
Produce a 10-slide executive version:
1. Keep the opening context slide and the final asks/decisions
   slide.
2. For the middle, keep only slides that carry a decision, a
   risk, or a result; merge supporting slides into speaker
   notes of the slide they support.
3. Add one new summary slide at the front: the three things a
   reader must take away.
Save as decks/full-project-review-exec-10.pptx; never modify
the original deck.
Preserve original slide numbers in each speaker note ("from
slides 12–14") so cuts are traceable. Do not soften or reword
any risk to make it fit — shorten around it.
```

*Why it works:* The keep/merge criteria and traceable slide references make the cut auditable — you can see exactly what was dropped and pull it back.

### 29. One-Slide Summary of a Project Folder

```
Read every file in projects/website-relaunch/ (status notes,
plans, budget spreadsheet, meeting notes).
Produce a single-slide project summary:
- Title: project name and today's date.
- Four quadrants: Status (on/off track, one sentence), Key
  numbers (max 3, each with source file), Risks (max 2), Next
  milestone with its date.
Put a one-paragraph narrative and the full source list in the
slide's speaker notes.
Save as projects/website-relaunch/one-slide-summary.pptx.
Use only what's in the folder — no outside knowledge. If the
files disagree on status or dates, show the most recent file's
version and flag the conflict in the speaker notes.
```

*Why it works:* The fixed quadrant layout with hard item caps forces prioritization — the model must choose the three numbers that matter, not list twenty.

### 30. Merge Team Decks into One Monthly Review Deck

```
Read every .pptx in decks/monthly/ (one deck per team) and the
agenda in decks/monthly/agenda.md.
Build one combined monthly review deck:
1. Order the sections to match agenda.md.
2. Per team: one divider slide, then a maximum of 3 slides
   condensed from that team's deck, keeping their strongest
   result and any risk they raised.
3. Close with one cross-team slide: shared risks or the same
   issue reported by more than one team.
Save as decks/monthly/monthly-review-combined-YYYY-MM.pptx.
Keep each team's own wording for their results — condense, don't
rewrite claims. Never modify the source decks. If a team listed
in agenda.md has no deck in the folder, add a placeholder slide
saying so instead of skipping the team silently.
```

*Why it works:* The missing-deck placeholder and "condense, don't rewrite" rules preserve accountability — every team is visibly present and owns its own claims.

## Research & Summarization — Claude Cowork Prompts

Prompts for synthesizing folders of notes and source documents into briefs, digests, and cited summaries — including parallel research tracks and version-diff reports, all files in, files out.

---

### 31. Monthly Competitive Change Briefing from a Competitor Notes Folder

```
Read every competitor subfolder in competitors/ and last month's
briefing in competitors/briefings/.
Produce this month's briefing:
1. Per competitor: WHAT CHANGED since last month (pricing,
   positioning, offers, notable content). If nothing changed,
   write one line saying so — do not pad.
2. SO WHAT: max 3 implications for us, each tied to a specific
   change above.
Save as competitors/briefings/competitive-brief-YYYY-MM.md,
matching the structure of last month's briefing.
Cite the source file for every factual claim. Label anything not
directly evidenced in the folder as "(inference)". If a competitor
subfolder is empty, flag it — don't fill the gap from memory.
```

*Why it works:* Anchoring on last month's briefing makes the output a delta report instead of a re-description, and the fact/inference split stops thin notes from becoming confident "facts".
*Part of the [14. Competitive Research Sweep](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/marketing/14-competitive-research-sweep.md) workflow.*

### 32. Single-Competitor Deep Dive Brief with Per-Claim File Citations

```
Read everything in competitors/acme-notes/ — meeting notes, saved
pages, screenshots, and any past write-ups.
Write a one-page profile covering: current positioning, pricing as
evidenced in the folder, apparent strengths, apparent weaknesses,
and open questions we can't answer from these files.
Save as competitors/acme-notes/profile-draft.md.
Keep it under 500 words; use the section headings above verbatim.
Cite the source file next to every factual claim. Separate facts
from inference — label anything you deduced as "(inference)".
List unknowns in "Open questions" rather than guessing; never
state something as market truth that appears in only one note.
```

*Why it works:* The mandatory "open questions" section gives the model a legitimate place to put uncertainty, so gaps get flagged instead of papered over.
*Part of the [14. Competitive Research Sweep](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/marketing/14-competitive-research-sweep.md) workflow.*

### 33. Summarize a Folder of Mixed Meeting Notes into a Decision Brief

```
Read every file in notes/project-alpha/ — a mix of meeting notes,
call summaries, and loose thoughts in .md, .txt, and .docx.
Produce a decision brief:
1. Decisions already made (with the file and date they appear in).
2. Open decisions still pending, with the options mentioned.
3. Action items, grouped by owner where an owner is named.
Save as notes/project-alpha/decision-brief.md.
Keep it under one page; bullets, not prose.
Cite the source file for every item. If two notes contradict each
other, list both versions with a [CONFLICT] tag — don't pick one.
If no owner is named for an action, mark it "(unassigned)" rather
than inferring one.
```

*Why it works:* Splitting "decided" from "still open" is the summarization business users actually need, and the [CONFLICT] tag converts messy-notes ambiguity into a reviewable list.

### 34. Synthesize Multiple Source Documents into a Cited Research Memo

```
Read all source documents in research/sources/ and the question I
need answered in research/question.md.
Write a memo that answers the question:
1. Direct answer in 3 sentences or fewer.
2. Supporting evidence — every claim followed by (source: filename,
   section or page).
3. Counter-evidence or dissenting sources, same citation format.
4. What the sources do NOT cover that the question needs.
Save as research/memo-draft.md.
Weigh sources by directness, not length — a table beats a vague
paragraph. Never present inference as a sourced fact: if you are
connecting dots across files, say "(synthesis, not stated in any
source)". If the sources can't answer the question, say so plainly
in section 1 instead of stretching weak evidence.
```

*Why it works:* Requiring a citation after every claim — plus a named label for cross-file synthesis — makes the memo auditable claim by claim, which is the difference between research and plausible prose.

### 35. Decompose a Research Question into Parallel Agent Tracks

```
Read research/brief.md and the materials in research/inputs/.
1. Decompose the brief into 3-4 research tracks that do NOT depend
   on each other's answers — state in one line why each is
   independent.
2. Run the tracks in parallel. Each track reads only its slice of
   research/inputs/ and writes its own file:
   research/tracks/track-N-<topic>.md — findings only, each with
   its source file, no recommendations yet.
3. Then, from the track files alone, write research/synthesis.md:
   one recommendation, three reasons, biggest risk, one page.
Every synthesis claim must cite a track file; every track claim
must cite a source file. Uncertainty labels (e.g. "client-stated",
"estimate") must survive from source to track to synthesis — if a
track drops one, fix the track before synthesizing.
```

*Why it works:* Separating findings-only track files from the synthesis step makes each track reviewable on its own, and the label-survival rule keeps hedged numbers from hardening into facts across hops.

### 36. What Changed Between Two Versions of a Long Document

```
Read docs/policy-v3.docx and docs/policy-v4-draft.docx.
Produce a change summary for reviewers who know v3 well:
1. Substantive changes — new obligations, removed clauses, altered
   numbers or dates — each with the section heading in both
   versions.
2. Wording-only changes, listed briefly in one block.
3. Sections that moved but did not change.
Save as docs/policy-v4-change-summary.md.
Order section 1 by likely impact, most significant first.
Quote the exact before/after text for every substantive change —
no paraphrased diffs. If you cannot tell whether a change is
substantive or cosmetic, put it in section 1 with a [JUDGMENT
CALL] tag. Do not modify either source document.
```

*Why it works:* Exact before/after quotes make every reported change verifiable in seconds, and the three-tier triage keeps reviewers focused on the changes that carry risk.

### 37. Weekly Reading-Pack Digest from a Folder of Saved Articles

```
Read every file in reading/inbox/ — saved articles, PDFs, and
pasted excerpts collected this week.
Build a digest:
1. One entry per source: 2-3 sentence summary, why it matters to
   our work, and the filename.
2. A "read in full" shortlist of at most 3 items, with one line on
   why each earned the slot.
3. Themes that appear in 2+ sources this week.
Save as reading/digests/digest-YYYY-MM-DD.md, then move nothing —
leave reading/inbox/ untouched.
Summaries must reflect only what each file says; don't blend in
outside knowledge of the topic. If a file is unreadable or
truncated, list it under "Could not process" instead of skipping
it silently.
```

*Why it works:* Capping the shortlist at 3 forces prioritization — the digest's real job — and the "could not process" rule ensures nothing drops out of the pipeline invisibly.

### 38. Extract Every Claim and Its Evidence from a Draft Report

```
Read the draft in reports/q2-draft.docx and all backing material
in reports/q2-sources/.
Build a claim audit:
1. Table with columns: claim (quoted from the draft), source file
   that supports it, strength (direct / partial / none found).
2. "None found" section: claims with no support in q2-sources/,
   flagged for the author.
3. Orphaned evidence: notable findings in the sources the draft
   never uses.
Save as reports/q2-claim-audit.md.
Quote claims verbatim — no paraphrasing that could soften them.
Do not edit the draft. "Partial" means the source supports a
weaker version of the claim; say what the source actually
supports. Never upgrade a claim's strength to be charitable.
```

*Why it works:* Running the audit as draft-versus-sources in both directions catches the two failure modes of reports — unsupported claims and buried evidence — in one pass.

### 39. Consolidate Interview Notes into a Findings Report with Quote Traceability

```
Read every interview file in research/interviews/ (one file per
conversation) and the guide in research/interview-guide.md.
Write a findings report:
1. Findings ordered by how many interviews support each — state
   the count and list the supporting filenames.
2. For each finding, 1-2 verbatim quotes with their source file.
3. Minority signals: things only one person said that still seem
   important, clearly marked as single-source.
Save as research/findings-report.md.
A finding needs support from at least 2 interview files; below
that it belongs in minority signals. Use only quotes that appear
word-for-word in the files — never compose a composite quote.
Don't infer what interviewees "probably meant"; if an answer is
ambiguous, note the ambiguity.
```

*Why it works:* The two-source threshold and verbatim-quote rule are the standard qualitative-research disciplines — encoding them in the prompt means the report arrives already defensible.

### 40. Rolling Research Log Update Without Rewriting History

```
Read the new material added this week to research/incoming/ and
the running log in research/research-log.md.
Append one new dated section to research-log.md:
1. New sources processed this week, one line each with filename.
2. What they add: confirmations, contradictions, or genuinely new
   information relative to the existing log.
3. Updated open-questions list — carry forward unanswered ones,
   strike through any this week's sources resolved (cite which).
Match the heading and date format of the existing log sections.
Append only — never rewrite or delete earlier sections, even to
fix their errors; note corrections in the new section instead.
Cite the incoming file for every point. If incoming/ is empty,
add a one-line "no new sources" entry and stop.
```

*Why it works:* Append-only with in-entry corrections preserves the audit trail of what you believed when, and framing new sources as confirm/contradict/new forces synthesis against prior knowledge instead of isolated summaries.

---
*Independent training resource. Not affiliated with or endorsed by Anthropic. Claude and Claude Cowork are trademarks of Anthropic, PBC.*

## Email & Communication — Claude Cowork Prompts

Prompts for drafting follow-up emails, weekly digests, status updates, and announcements from the meeting notes and project files already on your machine — every output lands as a reviewable draft file, never a sent message.

---

### 41. Draft a Client Follow-Up Email from Meeting Notes

```
Read the newest file in meeting-notes/ and the tone example in
examples/follow-up-example.md if it exists.
Draft a follow-up email to the external attendees:
- One line of thanks, no flattery.
- "What we agreed" — bullets, each with owner and date exactly as
  stated in the notes.
- "Next step" — one specific line.
Save as drafts/follow-up-YYYY-MM-DD.md. Match the example's tone;
keep it under 150 words.
Anything the notes mark [INTERNAL] must not appear in the draft.
Don't commit us to dates or deliverables not in the notes. This is
a draft for my review — never send anything.
```

*Why it works:* The [INTERNAL] exclusion and the "no invented commitments" rule are the two ways follow-up emails actually go wrong; both are handled before you read a word.
*Part of the [09. Follow-Up Email Drafter](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/09-follow-up-email-drafter.md) workflow.*

### 42. Write One External Follow-Up and One Internal Debrief from the Same Notes

```
Read the newest file in meeting-notes/.
Produce two separate drafts:
1. drafts/external-follow-up-YYYY-MM-DD.md — thanks, agreed items
   with owners and dates, next step. Under 150 words. Exclude
   anything marked [INTERNAL].
2. drafts/internal-debrief-YYYY-MM-DD.md — same agreed items plus
   the [INTERNAL] content, candid, for the team only.
Head each file with "AUDIENCE: EXTERNAL" or "AUDIENCE: INTERNAL".
If any line's audience is ambiguous, put it only in the internal
draft and flag it with [CHECK]. Draft files only — do not send,
and do not merge the two files.
```

*Why it works:* Splitting audiences into two named files with headers makes a copy-paste leak visible before it happens — the classic failure of mixed-audience notes.
*Part of the [09. Follow-Up Email Drafter](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/09-follow-up-email-drafter.md) workflow.*

### 43. Turn Raw Meeting Notes into an Action-Item Recap Email

```
Read the newest file in meeting-notes/.
Draft a recap email to the attendees with three sections:
1. ACTION ITEMS — task, owner, due date. If owner or date is not
   stated, write "UNASSIGNED" or "NO DATE" — do not infer them.
2. DECISIONS MADE — one line each.
3. OPEN QUESTIONS — raised but not resolved.
Save as drafts/recap-YYYY-MM-DD.md, with a short subject line at
the top. Keep it scannable — bullets, no paragraphs over 2 lines.
List every UNASSIGNED item again at the bottom under "Needs an
owner" so the gap is impossible to miss. Draft only — never send.
```

*Why it works:* The hard "do not infer owners" rule prevents phantom commitments — the recap surfaces gaps instead of papering over them with guesses.
*Part of the [07. Notes → Action Items](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/07-notes-to-action-items.md) workflow.*

### 44. Compress a Week of Standup Notes into a Manager-Ready Digest Email

```
Read all files in standups/ dated this week, plus last week's
digest in standups/digests/ if one exists.
Draft a digest email with four sections:
1. SHIPPED — completed items, grouped by person.
2. BLOCKED — every blocker, with how many days it has now
   appeared (check last week's digest for repeats).
3. LOAD — anyone stretched or on 3+ workstreams. Real signal
   looks like a person named with a number or a named third
   workstream — not "busy week!".
4. CHANGED — anything contradicting last week's digest.
Save as drafts/standup-digest-YYYY-MM-DD.md. Max one page, no
praise padding. Don't soften or omit blockers; if a standup file
for a weekday is missing, note it — don't fill the gap. Draft
only — I forward it myself.
```

*Why it works:* The repeat-counter on blockers and the calibrated LOAD example turn five days of fragments into the two signals a manager actually acts on.
*Part of the [08. Weekly Standup Digest](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/08-weekly-standup-digest.md) workflow.*

### 45. Draft a Pre-Meeting Context Email for Tomorrow's External Meetings

```
Read tomorrow's meetings from calendar-export.csv. For each one
involving someone outside our team, search clients/ and
meeting-notes/ for the most recent notes, open action items, and
unresolved issues involving them.
Draft one internal email I can send my team tonight: a max
one-paragraph briefing per meeting — attendees, where things
stand, open items with owners, one "don't forget" line — ordered
by meeting time.
Save as drafts/prep-email-YYYY-MM-DD.md. Skip internal 1:1s and
standups. If you find no history for a meeting, write "no prior
context found" — do not invent background. Draft only, and never
modify the source notes.
```

*Why it works:* "No prior context found" beats plausible-sounding invented background — the most dangerous failure a prep briefing can have.
*Part of the [06. Meeting Prep Pack](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/06-meeting-prep-pack.md) workflow.*

### 46. Write a Project Status-Update Email from the Project Folder

```
Read everything in projects/website-redesign/ — the plan, the
task list, and any notes or reports added in the last two weeks.
Draft a status email to the project sponsor:
1. One-line overall status: on track / at risk / off track, with
   the single fact that justifies it.
2. Done since last update, In progress, Blocked — bullets, each
   citing the source file.
3. What we need from the sponsor, if the files show anything.
Save as drafts/status-website-redesign-YYYY-MM-DD.md. Under 250
words, plain language, no jargon from the internal docs.
Don't promise dates that aren't in the plan; if files disagree on
a status, flag it with [CHECK] instead of picking one. Draft only.
```

*Why it works:* Forcing every bullet to cite its source file makes the update verifiable in one pass — the difference between a status report and a status guess.

### 47. Draft a Team Announcement Matching the Tone of a Past One

```
Read the announcement brief in comms/announcement-brief.md and
the past announcement in comms/examples/ that people responded
well to.
Draft the new announcement:
1. Match the example's structure, length, and tone exactly — same
   greeting style, same sign-off.
2. Cover every point in the brief; add nothing that isn't there.
3. End with the same kind of call-to-action the example used.
Save as drafts/announcement-DRAFT.md.
If the brief is missing a detail the example's structure needs
(a date, a name, a link), insert [MISSING: ...] rather than
guessing. This is a draft for review — never send or post it.
```

*Why it works:* Tone is learned from one real example, not adjectives — and [MISSING] placeholders keep gaps visible instead of silently filled.

### 48. Triage an Exported Inbox into Reply, Delegate, and Ignore Lists

```
Read the exported emails in inbox-export/ (one file per message,
or a single .csv/.mbox export).
Sort every message into three lists:
1. REPLY — needs my answer. Include sender, subject, the one
   question being asked, and a suggested one-line reply.
2. DELEGATE — someone else's call. Name who, only if the thread
   itself names them; otherwise mark "OWNER UNCLEAR".
3. IGNORE — newsletters, FYIs, resolved threads. One line why.
Save as triage/inbox-triage-YYYY-MM-DD.md, REPLY list first,
oldest waiting on top.
Suggested replies are drafts inside the file — never send or
reply to anything, and never delete or move the exported files.
```

*Why it works:* Triage is a sorting problem, not a writing problem — three named buckets plus "OWNER UNCLEAR" produce a work queue instead of forty open tabs.

### 49. Turn a Long Internal Document into a Short Stakeholder Email

```
Read reports/q3-operations-review.md (about 20 pages) and the
stakeholder list in team-context/stakeholders.md if it exists.
Draft an email version for non-technical stakeholders:
1. Subject line + a 3-sentence summary of what changed and why
   it matters to them.
2. Three bullets max of specifics, each citing the section of
   the source doc it came from.
3. One clear "what happens next" line — only if the document
   states one.
Save as drafts/stakeholder-brief-q3-ops.md. Under 200 words,
no internal acronyms. Don't editorialize or add reassurance the
document doesn't support; if the doc's conclusion is ambiguous,
say so rather than rounding it up to good news. Draft only.
```

*Why it works:* The "no unsupported reassurance" guardrail targets the summarizer's instinct to smooth bad news — stakeholder emails fail on spin, not length.

### 50. Draft Polite Reminder Emails for Overdue Action Items

```
Read action-items.md and today's date. Find every item whose due
date has passed and that isn't marked done.
For each overdue item's owner, draft one short reminder email:
- Reference the item, its original due date, and the meeting it
  came from (quote the source line from the file).
- Ask for a status or a new date — don't set one yourself.
- Neutral, blame-free tone: assume it slipped, not that they
  ignored it.
Save all drafts in one file: drafts/reminders-YYYY-MM-DD.md, one
section per owner. Skip items marked UNASSIGNED — list those at
the top under "Needs an owner first" instead of guessing a
recipient. Never send anything, and never edit action-items.md.
```

*Why it works:* Quoting the source line makes each nudge factual rather than accusatory, and refusing to invent new deadlines keeps the sender in control of commitments.

---
*Independent training resource. Not affiliated with or endorsed by Anthropic. Claude and Claude Cowork are trademarks of Anthropic, PBC.*

## Project Management — Claude Cowork Prompts

Prompts for running projects out of your files: action-item trackers built from meeting notes, status snapshots and risk logs pulled from project folders, folder audits, and plans drafted from briefs.

---

### 51. Turn Raw Meeting Notes into an Action Item Tracker

```
Read the newest file in meeting-notes/.
Extract three lists:
1. ACTION ITEMS — task, owner, due date. If the owner or date is
   not stated, write "UNASSIGNED" or "NO DATE" — do not infer
   them. Quote the source line under each item.
2. DECISIONS MADE — one line each.
3. OPEN QUESTIONS — anything raised but not resolved.
Append the action items to action-items.md under today's date,
keeping the existing format of that file.
Never mark an existing item in action-items.md as done unless
these notes explicitly say it was completed — quote the evidence.
```

*Why it works:* the "do not infer owners" rule plus the quoted source line turn every extracted item into a two-second verification instead of a phantom commitment.
*Part of the [07. Notes to Action Items](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/07-notes-to-action-items.md) workflow.*

### 52. Weekly Action Item Sweep Across All Meeting Notes

```
Read every file in meeting-notes/ dated within the last 7 days,
plus the current action-items.md.
1. Extract new action items (task, owner, due date) from each
   notes file, citing the file it came from.
2. Cross-check the existing tracker: mark items done only where
   a notes file explicitly says so, and quote that line.
3. List items past their due date with no status update.
Update action-items.md in place, adding a "Week of <date>"
section; keep its existing column layout.
Do not delete or rewrite existing entries — only append status
notes. Flag unowned items as UNASSIGNED rather than guessing.
```

*Why it works:* batching the week into one run keeps a single tracker authoritative, and the append-only rule means the tracker's history survives every run.
*Part of the [07. Notes to Action Items](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/meetings/07-notes-to-action-items.md) workflow.*

### 53. Project Folder Cleanup Plan with Rename and Archive Table

```
Read every filename and skim the contents of
projects/acme-launch/ — do not modify anything yet.
Produce cleanup-plan.md in that folder:
1. Proposed subfolder structure (by phase, document type, date).
2. Rename table: current name → proposed name, one row per file.
3. Duplicates and near-duplicates: group them, recommend a keeper
   (newest, most complete, or explicitly marked final) and why.
4. "Needs a human": any file whose purpose or current version you
   cannot determine — never guess which version is current.
Follow naming-convention.md if it exists; otherwise propose a
convention at the top of the plan.
Do not rename, move, or delete anything until I approve the plan.
```

*Why it works:* the plan-then-approve gate converts a destructive cleanup into a reviewable document — the file named FINAL is often older than the unlabeled v2.
*Part of the [13. Asset Folder Cleanup](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/marketing/13-asset-folder-cleanup.md) workflow.*

### 54. Build a Project Status Snapshot from the Project Folder

```
Read everything in projects/acme-launch/ — the plan, meeting
notes, action-items.md, and any status emails saved as files.
Build a one-page status snapshot:
1. Where the project stands vs. the milestones in plan.md.
2. Top 5 open action items with owners and due dates.
3. Risks or blockers mentioned in the last two weeks of notes.
4. Decisions still waiting on someone — name who, per the files.
Output as projects/acme-launch/status-snapshot.md, under 300
words, each claim followed by the source file in parentheses.
If the files disagree about a milestone's status, show both
versions with [CONFLICT: ...] — do not pick one. Do not report
anything as complete without a file that says so.
```

*Why it works:* forcing a source citation on every claim makes the snapshot auditable, so a wrong status gets caught at review instead of in the steering meeting.

### 55. Extract a Risk Log from Project Notes and Documents

```
Read all files in projects/acme-launch/notes/ and the current
plan in projects/acme-launch/plan.md.
Build a risk log:
1. Extract every risk, blocker, concern, or "worried about"
   mention — including ones raised in passing.
2. For each: description, first-mentioned date, source file and
   quoted line, current status (open/mitigated/unclear).
3. Group duplicates that describe the same underlying risk.
Output as projects/acme-launch/risk-log.md, one table, sorted
with open risks first.
Do not rate severity or invent mitigations — leave a blank
"Mitigation" column for the team. If a risk's status is not
stated in the files, mark it "unclear", not "closed".
```

*Why it works:* risks die in meeting notes; sweeping them into one dated, quoted table surfaces the ones raised weeks ago that nobody wrote down twice.

### 56. Audit a Project Folder for Stale and Missing Documents

```
Read the file list and modification dates in projects/acme-launch/
and compare against the expected documents listed in
project-checklist.md (brief, plan, budget, status reports,
sign-offs).
Produce projects/acme-launch/folder-audit.md with three sections:
1. MISSING — expected documents with no matching file.
2. STALE — files untouched for 30+ days that the plan says
   should be updated regularly (status reports, trackers).
3. UNKNOWN — files in the folder that match nothing on the
   checklist; describe each in one line from its contents.
Report only — do not create placeholder files, and do not move
or delete anything. If project-checklist.md is missing, stop
and say so instead of inventing an expected list.
```

*Why it works:* auditing against a named checklist instead of "what looks missing" makes the gaps objective — and the stop-if-no-checklist rule prevents an invented standard.

### 57. Draft a Project Kickoff Plan from a Brief

```
Read projects/acme-launch/brief.md and, as a structure example,
templates/kickoff-plan-example.md.
Draft a kickoff plan:
1. Objective and scope, restated from the brief in plain terms.
2. Workstreams with a proposed sequence and rough phases.
3. Roles needed — as roles, not names, unless the brief names
   people.
4. Open questions the brief does not answer, as a list for the
   kickoff meeting.
Output as projects/acme-launch/kickoff-plan-draft.md, matching
the example's section structure, under 600 words.
Do not invent deadlines, budgets, or headcount not in the brief —
where the brief is silent, write [TBD: <what's needed>].
```

*Why it works:* the [TBD] convention turns the brief's gaps into a ready-made kickoff agenda instead of plausible-looking invented commitments.

### 58. Weekly "What Changed" Project Digest

```
Read every file in projects/acme-launch/ modified in the last 7
days, plus last week's digest at
projects/acme-launch/digests/ (newest file) for comparison.
Write this week's digest:
1. CHANGED — documents updated this week and what changed in
   each, in one line.
2. PROGRESS — action items completed or milestones passed, with
   the source file.
3. NEW — risks, decisions, or scope items that appeared this week.
Output as projects/acme-launch/digests/digest-<YYYY-MM-DD>.md,
same section structure as last week's, under 250 words.
Do not modify the source files or previous digests. If nothing
changed in a section, write "No changes" — do not pad it.
```

*Why it works:* scoping the read to files modified this week keeps the run fast and the digest honest — it can only report what actually moved.

### 59. Reconcile the Project Plan Against Actual Progress

```
Read projects/acme-launch/plan.md, action-items.md, and the last
four files in projects/acme-launch/notes/.
Compare plan vs. reality:
1. For each milestone in the plan: on track, late, done, or no
   evidence either way — with the source line that shows it.
2. Work happening in the notes that maps to no plan milestone
   (scope creep candidates).
3. Plan items no file has mentioned in 30+ days (silent stalls).
Output as projects/acme-launch/plan-vs-actual.md, one table per
section.
Do not edit plan.md or reschedule anything — this is a findings
report. Where evidence is ambiguous, put the item under "no
evidence", not under "done".
```

*Why it works:* the "no evidence" bucket is the point — it separates milestones that are actually done from milestones everyone merely assumes are done.

### 60. Roll Up Multiple Project Statuses into a Portfolio Summary

```
Read the latest status-snapshot.md (or equivalent status file)
in each subfolder of projects/ — one subfolder per project.
Build a portfolio summary:
1. One row per project: name, phase, overall health as stated in
   its own status file, next milestone, top risk.
2. A "needs attention" list: projects whose status file is
   missing or older than 14 days.
3. Cross-project conflicts: the same person or resource
   committed in two projects at once, per the files.
Output as projects/portfolio-summary.md with the table first.
Use each project's own stated health — do not upgrade or
downgrade it yourself. Never fill a cell by assumption: missing
information stays blank with a note in "needs attention".
```

*Why it works:* letting each project's own status file speak — and flagging silence instead of papering over it — makes the rollup a control instrument rather than a reassurance memo.

## Team Workflows & Knowledge — Claude Cowork Prompts

Single-run versions of the full [team workflows](https://github.com/claude-cowork-training/claude-cowork-team-workflows): onboarding plans, context folders, glossaries, playbooks, and FAQs built from the documents your team already has.

---

### 61. Generate a New Hire's First-Week Plan from Team Docs

```
Read team-context/, onboarding/checklist.md, and the role
description in onboarding/roles/analyst.md.
Create onboarding/plans/new-hire-week-1.md with:
1. A day-by-day schedule for week one — checklist items placed
   sensibly (accounts before tools, context before clients).
2. A reading list from team-context/, ordered by relevance to
   this role, with one line on why each file matters.
3. People to meet, drawn from about-your-team.md, with what to
   ask each person.
4. One small real task completable by Friday, taken from the
   role file's responsibilities.
Only reference files and people that actually appear in these
folders. If the role file is thin, flag the gap — don't invent
responsibilities. No personal data beyond names and roles.
```

*Why it works:* the only-what-exists guardrail is the whole trick — without it, thin role files get padded with invented duties nobody agreed to.
*Part of the [21. New Hire First-Week Plan](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/21-new-hire-first-week-plan.md) workflow.*

### 62. Turn a First-Week Plan into a 30/60/90 Ramp Plan

```
Read onboarding/plans/new-hire-week-1.md, team-context/, and
onboarding/roles/analyst.md.
Extend the week-one plan into onboarding/plans/new-hire-90-day.md:
1. Month 1: learning goals tied to specific team-context files
   and the week-one reading list.
2. Month 2: increasing ownership — which recurring tasks from
   team-context/playbooks/ this role starts running.
3. Month 3: full-ownership milestones with a measurable "done"
   for each, drawn from the role file.
Keep each month to one page. Every milestone must trace to a
responsibility in the role file or a playbook that exists —
flag months that lack material rather than filling them with
generic goals like "build relationships".
```

*Why it works:* forcing every milestone to trace to an existing file converts a motivational template into a checkable plan.
*Part of the [21. New Hire First-Week Plan](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/21-new-hire-first-week-plan.md) workflow.*

### 63. Build a Team Context Folder from Existing Documents

```
Read the representative documents in samples/ (reports, emails,
docs the team considers "how we sound").
Draft a team context folder in team-context/ with three files:
1. about-your-team.md — who we are, what we make, who we serve,
   as far as the samples show it.
2. style-guide.md — writing rules evidenced by the samples:
   tone, formats, structures, recurring conventions.
3. glossary.md — only terms a smart outsider would misunderstand,
   each with a definition inferred from usage.
Every style rule must cite the sample that evidences it — no
generic filler like "be clear and professional". Mark anything
you inferred but couldn't verify with [CONFIRM] so I can review
before the team adopts the folder.
```

*Why it works:* the evidence rule blocks the classic failure — a context folder of rules that describe every company on earth and teach Cowork nothing.
*Part of the [22. Team Context Folder Builder](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/22-team-context-folder-builder.md) workflow.*

### 64. Quarterly Team Context Refresh as a Reviewable Diff

```
Read everything in team-context/ and this quarter's new
documents in samples/recent/.
Propose updates to the context folder as a change list, not a
rewrite. Output team-context/updates/context-diff-2026-q3.md:
1. ADD — rules, terms, or facts the recent documents establish
   that the context folder lacks (cite the source document).
2. UPDATE — context lines the recent documents contradict, with
   both versions quoted side by side.
3. REMOVE CANDIDATES — context lines no recent document supports
   anymore, listed for a human call.
Do not edit any file in team-context/ directly. Where old and
new documents conflict, present both — never silently pick the
newer one as truth.
```

*Why it works:* a diff you approve keeps the folder maintained; a rewrite you have to re-read from scratch guarantees it rots instead.
*Part of the [22. Team Context Folder Builder](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/22-team-context-folder-builder.md) workflow.*

### 65. Extract a Team Glossary from Real Internal Documents

```
Read every document in samples/ and the existing
team-context/glossary.md if present.
Find every term a smart new hire would not understand: acronyms,
internal nicknames, product and process names, ordinary words
used with a non-obvious specific meaning.
For each term not already in the glossary, draft an entry with:
- the term
- a definition inferred from usage, labeled CONFIDENT (usage
  makes it unambiguous) or GUESS (team should verify)
- 1–2 direct quotes from the source documents showing it in use
Exclude standard industry terms any professional would know.
Output as glossary-additions-2026-07.md for review — do not edit
the main glossary directly, and never present a GUESS definition
without its label.
```

*Why it works:* the confidence label plus source quotes is what stops a plausible-but-wrong definition from quietly becoming what new hires are taught.
*Part of the [23. Glossary Extractor](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/23-glossary-extractor.md) workflow.*

### 66. Write a Playbook for a Recurring Task from Its Past Outputs

```
Read the past outputs of our weekly status digest in examples/
and anything relevant in team-context/.
Draft a playbook so someone who has never done this task could
run it. Structure: Trigger · Owner · Inputs (exact file
locations) · Output (name, format, destination) · Standards ·
Known failures and what to do about them.
Infer cadence, format, and quality standards from the examples;
quote the example that evidences each standard.
Save as team-context/playbooks/weekly-digest-playbook.md.
Where the examples don't reveal a step (what triggers the task,
what goes wrong), write [ASK OWNER: question] instead of
guessing — a confident invented step is worse than a visible
gap.
```

*Why it works:* mandating [ASK OWNER] markers turns the inevitable unknowns into an interview agenda instead of silent fabrication.
*Part of the [24. Playbook Writer](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/24-playbook-writer.md) workflow.*

### 67. Build a Sourced Team FAQ from Actually-Asked Questions

```
Read all of team-context/, the collected real questions in
questions/, and the existing faq.md if present.
Produce faq-update-2026-07.md:
1. For each new question: a concise answer sourced ONLY from
   team-context documents, with the source file named under
   each answer.
2. Questions no document answers go under "DOCUMENTATION GAPS"
   with a suggested home for the missing answer.
3. Group Q&As by theme; merge duplicates but keep the phrasing
   people actually used.
4. STALE CHECK: flag existing FAQ answers that contradict the
   current team-context files.
Answers must not go beyond what the documents say — a confident
wrong answer in an FAQ is worse than an honest gap.
```

*Why it works:* the documents-only rule prevents the FAQ from inventing policy that then becomes real by accident.
*Part of the [25. FAQ Builder from Team Docs](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/25-faq-builder-from-team-docs.md) workflow.*

### 68. Answer New-Hire Questions from the Context Folder Only

```
Read team-context/ in full, then read the new hire's questions
in onboarding/questions-week-1.md.
For each question, write one of exactly two things:
1. An answer drawn from a team-context file, with the file and
   the relevant line quoted beneath it.
2. "NOT DOCUMENTED" plus which context file this answer should
   live in once someone writes it.
Output as onboarding/answers-week-1.md, questions in their
original order and original wording.
Never blend general knowledge into an answer to fill a gap —
the NOT DOCUMENTED list is the deliverable that tells us what
the folder is missing, so don't shrink it.
```

*Why it works:* the binary answered/not-documented format makes documentation gaps impossible to paper over — the gap list is the real output.
*Part of the [25. FAQ Builder from Team Docs](https://github.com/claude-cowork-training/claude-cowork-team-workflows/blob/main/workflows/onboarding-knowledge/25-faq-builder-from-team-docs.md) workflow.*

### 69. Audit a Team Context Folder for Gaps and Staleness

```
Read everything in team-context/ and, for comparison, the last
three months of real output in reports/ and client-docs/.
Audit the context folder and write team-context/audit-report.md:
1. STALE — context lines the recent output contradicts (quote
   both sides; a folder describing last year is worse than none).
2. UNUSED — glossary terms and style rules that no recent
   document reflects; candidates for deletion.
3. MISSING — conventions the recent output follows consistently
   that no context file documents.
4. FILLER — lines that would change no output (test each rule:
   name a document it would alter; if you can't, list it here).
Do not modify any context file. Where you're unsure whether a
rule is stale or the recent docs are just sloppy, say so — flag,
don't rule.
```

*Why it works:* the earn-its-place test ("name an output this line would change") is the sharpest known filter for context-folder filler.

### 70. Document a Recurring Task as a Shareable Four-Field Workflow

```
I run a recurring task I want teammates to run without me. Read
its recent inputs in monthly-inputs/ and my last three outputs
in archive/.
Document it to this four-field standard, all files in / files
out:
- INPUTS: every file the task reads, exact paths, and what each
  contributes.
- STEPS: numbered, in order, each naming the file it reads or
  writes — no step may depend on knowledge that isn't in a file.
- OUTPUT: exact filename, format, and destination folder.
- CHECKS: how the runner verifies the output is right before
  sending, based on what my three archived outputs have in
  common.
Save as team-context/workflows/monthly-task-workflow.md. If any
step requires information that lives only in my head, mark it
[UNDOCUMENTED DEPENDENCY] — those markers are the point.
```

*Why it works:* "no step may depend on knowledge that isn't in a file" is the bus-factor test — every violation it surfaces is exactly what would break the handover.

---
*Independent training resource. Not affiliated with or endorsed by Anthropic. Claude and Claude Cowork are trademarks of Anthropic, PBC.*

---

## License & attribution

Content licensed [CC BY 4.0](LICENSE): use these prompts at work, share them, adapt them — just credit [claudecoworktraining.com](https://claudecoworktraining.com), where the full written guides and [live team training](https://claudecoworktraining.com/teams/training/) live.

*Independent training resource. Not affiliated with or endorsed by Anthropic. Claude and Claude Cowork are trademarks of Anthropic, PBC.*
