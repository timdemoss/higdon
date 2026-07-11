---
name: quiz
description: After completing substantial work, generate an HTML report of what was done plus a quiz that tests whether the user actually understands it — the gate for merging, sending, or shipping is passing the quiz clean. Works for any deliverable, not just code (a contract, a plan, a filing, an application). Use after nontrivial work, or when the user invokes /quiz.
---

# Work Report + Quiz

The user shouldn't ship what they couldn't explain — merge the code, sign the contract, send the application. Produce an HTML report of the work just completed, followed by a quiz, and grade their answers. The bar: don't ship until the quiz is passed without errors.

Scope: $ARGUMENTS (if empty, use the work just completed in this session; for code, the current branch's diff against the default branch)

## Steps

1. **Build the report.** Walk the actual work product — the real diff, the final document, the submitted materials — don't work from memory of what you intended. The report covers: what was done and why (grouped by concern, not by file or chronology), the decisions and trade-offs embedded in it (pull from the decision log / implementation-notes.md if one exists), what someone on the receiving end would notice changed, and what was deliberately NOT done.

2. **Write the quiz — 5 to 8 questions.** Test understanding that matters for living with this work, not trivia:
   - "What happens if X?" questions about consequences and edge cases (for code: new behavior; for a contract or plan: obligations and contingencies)
   - "Why was Y chosen over Z?" for the real trade-offs
   - At least one question about a failure mode, limitation, or risk of the work
   - Nothing answerable by pattern-matching the report's headings; no filename, page-number, or date trivia
   Multiple choice with plausible distractors, answers hidden behind a reveal (`<details>` or a button).

3. **Deliver as a single self-contained HTML page** via the Artifact tool (load the artifact-design skill first): report on top, quiz below. Style for reading, not decoration.

4. **Grade.** When the user gives their answers, grade them. Full marks: say it's ready to ship. Any miss: explain the misses against the relevant part of the work, then offer a fresh variant of the missed questions. Do not soften the gate — a miss means the work isn't understood yet.
