# Team Workflows & Knowledge — Claude Cowork Prompts

Single-run versions of the full [team workflows](https://github.com/claude-cowork-training/claude-cowork-team-workflows): onboarding plans, context folders, glossaries, playbooks, and FAQs built from the documents your team already has.

---

## 61. Generate a New Hire's First-Week Plan from Team Docs

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

## 62. Turn a First-Week Plan into a 30/60/90 Ramp Plan

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

## 63. Build a Team Context Folder from Existing Documents

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

## 64. Quarterly Team Context Refresh as a Reviewable Diff

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

## 65. Extract a Team Glossary from Real Internal Documents

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

## 66. Write a Playbook for a Recurring Task from Its Past Outputs

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

## 67. Build a Sourced Team FAQ from Actually-Asked Questions

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

## 68. Answer New-Hire Questions from the Context Folder Only

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

## 69. Audit a Team Context Folder for Gaps and Staleness

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

## 70. Document a Recurring Task as a Shareable Four-Field Workflow

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
