# Spreadsheets & Data — Claude Cowork Prompts

Prompts for cleaning, deduplicating, reconciling, and summarizing CSV files and spreadsheet exports — messy data in, reviewable files out.

---

## 11. Match Two Exports and Produce an Exception Report

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

## 12. Clean a Raw Expense CSV and Build a Missing-Items Chase List

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

## 13. Turn a Pipeline CSV into a Meeting-Ready Stale-Leads Summary

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

## 14. Build an Invoice Aging Table from a Folder of Invoices

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

## 15. Summarize Multi-Channel Campaign CSVs into One Performance Table

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

## 16. Deduplicate a Contact CSV Without Losing Any Data

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

## 17. Merge Monthly CSV Exports into One Master File

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

## 18. Normalize Mixed Date Formats Across a Spreadsheet Export

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

## 19. Pivot-Style Summary of a Transactions CSV by Category and Month

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

## 20. Compare Two Versions of a Spreadsheet and Report What Changed

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
