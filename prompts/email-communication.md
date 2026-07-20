# Email & Communication — Claude Cowork Prompts

Prompts for drafting follow-up emails, weekly digests, status updates, and announcements from the meeting notes and project files already on your machine — every output lands as a reviewable draft file, never a sent message.

---

## 41. Draft a Client Follow-Up Email from Meeting Notes

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

## 42. Write One External Follow-Up and One Internal Debrief from the Same Notes

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

## 43. Turn Raw Meeting Notes into an Action-Item Recap Email

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

## 44. Compress a Week of Standup Notes into a Manager-Ready Digest Email

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

## 45. Draft a Pre-Meeting Context Email for Tomorrow's External Meetings

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

## 46. Write a Project Status-Update Email from the Project Folder

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

## 47. Draft a Team Announcement Matching the Tone of a Past One

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

## 48. Triage an Exported Inbox into Reply, Delegate, and Ignore Lists

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

## 49. Turn a Long Internal Document into a Short Stakeholder Email

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

## 50. Draft Polite Reminder Emails for Overdue Action Items

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
