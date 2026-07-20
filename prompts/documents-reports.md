# Documents & Reports — Claude Cowork Prompts

Prompts for drafting, updating, and assembling business documents and reports — KPI summaries, monthly reports, status digests, close packages, and variance commentary — directly from the files in your folders.

---

## 01. Write a weekly KPI report from a metrics CSV and last week's report

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

## 02. Draft a monthly business report from metrics, notes, and last month's example

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

## 03. Build a weekly client status digest from a folder of meeting notes

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

## 04. Assemble a monthly close report from a folder of finance exports

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

## 05. Draft variance commentary comparing actuals to budget spreadsheets

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

## 06. Update an existing report with this month's numbers without touching the prose

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

## 07. Turn a folder of meeting notes into a project status report

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

## 08. Condense a long report into a one-page executive brief

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

## 09. Draft a client proposal by reusing sections from past winning proposals

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

## 10. Standardize a folder of mixed-format documents against a house template

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
