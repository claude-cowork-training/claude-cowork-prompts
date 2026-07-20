# Research & Summarization — Claude Cowork Prompts

Prompts for synthesizing folders of notes and source documents into briefs, digests, and cited summaries — including parallel research tracks and version-diff reports, all files in, files out.

---

## 31. Monthly Competitive Change Briefing from a Competitor Notes Folder

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

## 32. Single-Competitor Deep Dive Brief with Per-Claim File Citations

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

## 33. Summarize a Folder of Mixed Meeting Notes into a Decision Brief

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

## 34. Synthesize Multiple Source Documents into a Cited Research Memo

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

## 35. Decompose a Research Question into Parallel Agent Tracks

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

## 36. What Changed Between Two Versions of a Long Document

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

## 37. Weekly Reading-Pack Digest from a Folder of Saved Articles

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

## 38. Extract Every Claim and Its Evidence from a Draft Report

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

## 39. Consolidate Interview Notes into a Findings Report with Quote Traceability

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

## 40. Rolling Research Log Update Without Rewriting History

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
