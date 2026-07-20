# Presentations & Decks — Claude Cowork Prompts

Prompts for building, refreshing, condensing, and auditing slide decks straight from the reports, metrics files, and project folders you already have.

---

## 21. Refresh Last Period's Board Deck with This Period's Numbers

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

## 22. Build a Client QBR Deck from the Quarter's Folder

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

## 23. Turn an Engagement Folder into a Case Study Deck

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

## 24. Audit a Deck for Numbers with No Source File

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

## 25. Turn a Written Report into a Slide Deck

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

## 26. Generate Speaker Notes for Every Slide in a Deck

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

## 27. Deck Consistency Audit Before It Ships

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

## 28. Condense a 30-Slide Deck into a 10-Slide Executive Version

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

## 29. One-Slide Summary of a Project Folder

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

## 30. Merge Team Decks into One Monthly Review Deck

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
