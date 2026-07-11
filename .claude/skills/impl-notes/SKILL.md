---
name: impl-notes
description: Keep a running decision log during a substantial task — decisions made, deviations from the plan, and surprises — so they can be reviewed and learned from. Works for any long-running work, not just coding (research, applications, planning, writing). Use when starting nontrivial work, or when the user invokes /impl-notes.
---

# Implementation Notes / Decision Log

For the duration of the current task, maintain a running decision log. With filesystem access, keep it as a temporary `implementation-notes.md` in the working directory (git-ignore it or delete it before merge unless the user wants it kept). Without a filesystem, keep a clearly-marked "Decision log" section that you carry forward and update in your replies.

## What to log

Append an entry whenever one of these happens — not for routine progress:

- **A decision the plan didn't cover.** What came up, the options, which you chose, and why.
- **A deviation from the plan or prompt.** What the plan said, what you did instead, and the evidence that forced the change.
- **An unexpected complication.** When one appears mid-task: pick the conservative option (the one easiest to reverse), log it here with the alternatives, and keep working — do not stall the task on it. Flag entries that deserve the user's review with `⚠`.
- **Something learned that invalidates an assumption** from the brief, interview, or blindspot pass.

Entry format: one short paragraph, timestamped, written for someone rereading it next week — no shorthand that only makes sense mid-task.

## At the end of the task

Summarize the notes in your final reply: decisions made, `⚠` items needing the user's judgment, and anything that should change the next prompt or the plan for a follow-up attempt. If the task went sideways, these notes are the input for a better-specified retry — say explicitly what the retry prompt should include that the original didn't.
