# Project Management — Claude Cowork Prompts

Prompts for running projects out of your files: action-item trackers built from meeting notes, status snapshots and risk logs pulled from project folders, folder audits, and plans drafted from briefs.

---

## 51. Turn Raw Meeting Notes into an Action Item Tracker

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

## 52. Weekly Action Item Sweep Across All Meeting Notes

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

## 53. Project Folder Cleanup Plan with Rename and Archive Table

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

## 54. Build a Project Status Snapshot from the Project Folder

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

## 55. Extract a Risk Log from Project Notes and Documents

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

## 56. Audit a Project Folder for Stale and Missing Documents

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

## 57. Draft a Project Kickoff Plan from a Brief

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

## 58. Weekly "What Changed" Project Digest

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

## 59. Reconcile the Project Plan Against Actual Progress

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

## 60. Roll Up Multiple Project Statuses into a Portfolio Summary

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
