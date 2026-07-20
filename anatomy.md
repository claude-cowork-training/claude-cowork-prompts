# The Anatomy of a Good Cowork Prompt

Every prompt in this library follows the same 5-part frame. It exists because Claude Cowork is not a chat window — it's an agent working in your actual files and folders, and the prompts that work treat it that way. If a prompt would work identically pasted into a chat window, it doesn't belong here.

## The 5 parts

### 1. Inputs — point at real files
Tell Cowork exactly what to read: a folder, specific files, or a pattern.

> *"Read every file in reports/2026-q2/ and the notes in review-notes.md…"*

Vague inputs ("look at my reports") force Cowork to guess scope. Named inputs make the run reproducible — same files in, same shape out.

### 2. Task — one job, with its steps
Say what to do, in order, when order matters. Numbered steps beat prose for multi-step work — Cowork follows a list more faithfully than a paragraph.

> *"1. Extract every figure with its source file. 2. Compare against last month. 3. Flag anything >10% off."*

### 3. Output — name the artifact
Cowork's advantage is that it *produces files*. Say which format, which filename, where it goes.

> *"Output as a .docx: reports/drafts/q2-summary.docx."*

A prompt that ends without an output spec ends in a chat reply — which usually means you'll do the formatting work yourself anyway.

### 4. Standards — what "good" looks like
Reference an example, a style guide, or explicit criteria. This is the highest-leverage line in most prompts.

> *"Match the structure and tone of reports/examples/last-month.docx. Keep the summary under 200 words."*

Teams that maintain a shared context folder (style guide, glossary, examples) can compress this part to one line: *"Follow style-guide.md."* That's the core idea behind the [team workflows](https://github.com/claude-cowork-training/claude-cowork-team-workflows).

### 5. Guardrails — what NOT to do
The part most prompts skip, and the part that separates a usable draft from a silent mess. Tell Cowork what to leave alone, when to stop, and how to handle the unexpected.

> *"Never delete or modify the source files. If a figure appears in two files with different values, don't pick one — flag it. If an expected file is missing, stop and list what's missing."*

Agents are helpful by default; guardrails convert unwanted helpfulness (silent "corrections," invented numbers, destructive cleanup) into flags you can review.

## A complete example

```
Read every file in scenarios/report-inputs/ (a CSV of monthly metrics,
notes from the team lead, and last month's report).

Draft this month's report:
1. Follow the exact section structure of last-month-report-example.md.
2. Pull every number from monthly-metrics.csv — cite the row you used.
3. Work the context from notes-from-dana.md into the narrative.

Output as report-draft.md in this folder.

Match the tone of the example report; keep each section under 150 words.

Don't invent numbers that aren't in the CSV. If the notes contradict
the data, flag it with [CHECK: ...] instead of resolving it yourself.
```

Inputs (a named folder and its files) → Task (three ordered steps) → Output (a named file) → Standards (the example + length limit) → Guardrails (no invented numbers, contradictions flagged).

## Using the frame

- **Adapting a library prompt:** swap the file paths and standards for your own; keep the guardrails — they're usually the part that took the most testing.
- **Writing your own:** draft the five parts in order, then read only your guardrails and ask "what's the worst thing an eager assistant could do here?" Add what's missing.
- **When a prompt misbehaves:** the fix is almost always a missing part — usually Standards (output was fine but wrong shape) or Guardrails (output was confident but wrong).

Want the interactive version? [The free Cowork course](https://github.com/claude-cowork-training/cowork-course) teaches this frame with hands-on exercises, and [claudecoworktraining.com](https://claudecoworktraining.com) has the full written guides.

---
*Independent training resource. Not affiliated with or endorsed by Anthropic. Claude and Claude Cowork are trademarks of Anthropic, PBC.*
