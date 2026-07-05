---
name: impl-notes
description: Keep a running implementation-notes.md during a coding task — log decisions, deviations from the plan, and surprises so they can be reviewed and learned from. Use when starting a nontrivial implementation, or when the user invokes /impl-notes.
---

# Implementation Notes

For the duration of the current implementation task, maintain a temporary `implementation-notes.md` at the repo root (git-ignore it or delete it before merge unless the user wants it kept).

## What to log

Append an entry whenever one of these happens — not for routine progress:

- **A decision the plan didn't cover.** What came up, the options, which you chose, and why.
- **A deviation from the plan or prompt.** What the plan said, what you did instead, and the evidence that forced the change.
- **An unexpected edge case.** When one appears mid-implementation: pick the conservative option (the one easiest to reverse), log it here with the alternatives, and keep working — do not stall the task on it. Flag entries that deserve the user's review with `⚠`.
- **Something learned that invalidates an assumption** from the brief, interview, or blindspot pass.

Entry format: one short paragraph, timestamped, written for someone rereading it next week — no shorthand that only makes sense mid-task.

## At the end of the task

Summarize the notes in your final reply: decisions made, `⚠` items needing the user's judgment, and anything that should change the next prompt or the plan for a follow-up attempt. If the task went sideways, these notes are the input for a better-specified retry — say explicitly what the retry prompt should include that the original didn't.
