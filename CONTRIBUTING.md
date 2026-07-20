# Contributing a prompt

New prompts are welcome — the goal is a library people actually run, so the bar is "tested and Cowork-native," not "sounds clever."

## The rules (all four required)

1. **Cowork-native.** The prompt must reference files, folders, or output artifacts ("Read every file in /reports, then… Output as .docx…"). If it would work identically pasted into a chat window, it belongs in a generic prompt list, not here.
2. **Complete anatomy.** All five parts from [`anatomy.md`](anatomy.md): Inputs, Task, Output, Standards, Guardrails. Reviewers check the guardrails first — a prompt with no "what not to do" line isn't done.
3. **Tested.** You ran it in Claude Cowork at least once before opening the PR. Say so in the PR description and note anything that surprised you.
4. **Synthetic examples only.** Generic folder/file names or fictional data — no real company names, client data, or personal information.

## How

1. Match the exact format of any existing prompt: `## NN. Name` · the prompt in a code block · one-line *Why it works*.
2. Add it to the matching category file in [`prompts/`](prompts/) using the next free number, and mirror it into the README's inline list.
3. If your prompt is a single-run slice of one of the [team workflows](https://github.com/claude-cowork-training/claude-cowork-team-workflows), add the "Part of the … workflow" link.
4. Add a line to [`CHANGELOG.md`](CHANGELOG.md).
5. Open a PR. We respond within 48 hours.

## Fixes and improvements

Typos, tighter guardrails, better "why it works" lines — just open a PR. If a prompt stopped working because Cowork's behavior changed, that's the most valuable PR of all: describe what changed and include your fixed prompt.

By contributing you agree your contribution is licensed under [CC BY 4.0](LICENSE).
