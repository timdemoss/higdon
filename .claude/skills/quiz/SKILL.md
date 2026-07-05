---
name: quiz
description: After an implementation, generate an HTML report of what changed plus a quiz that tests whether the user actually understands the changes — the merge gate is passing the quiz clean. Use after completing a nontrivial change, or when the user invokes /quiz.
---

# Change Report + Quiz

The user shouldn't merge code they couldn't explain. Produce an HTML report of the changes just made, followed by a quiz, and grade their answers. The bar: don't merge until the quiz is passed without errors.

Scope: $ARGUMENTS (if empty, use the current branch's diff against the default branch)

## Steps

1. **Build the report.** Walk the actual diff — don't work from memory of what you intended. The report covers: what changed and why (grouped by concern, not by file), the decisions and trade-offs embedded in the changes (pull from implementation-notes.md if one exists), behavior changes a user or caller would notice, and what was deliberately NOT done.

2. **Write the quiz — 5 to 8 questions.** Test understanding that matters for maintaining this code, not trivia:
   - "What happens if X?" questions about the new behavior and its edge cases
   - "Why was Y chosen over Z?" for the real trade-offs
   - At least one question about a failure mode or limitation of the change
   - Nothing answerable by pattern-matching the report's headings; no filename or line-number trivia
   Multiple choice with plausible distractors, answers hidden behind a reveal (`<details>` or a button).

3. **Deliver as a single self-contained HTML page** via the Artifact tool (load the artifact-design skill first): report on top, quiz below. Style for reading, not decoration.

4. **Grade.** When the user gives their answers, grade them. Full marks: say it's ready to merge. Any miss: explain the misses against the relevant part of the diff, then offer a fresh variant of the missed questions. Do not soften the gate — a miss means the change isn't understood yet.
