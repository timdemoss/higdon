---
name: interview
description: Structured interview to turn a fuzzy idea into a buildable spec — ask the user one question at a time, prioritized by architectural impact. Use when the user has a task in mind but hasn't pinned down the requirements, or invokes /interview.
---

# Structured Interview

The user has a task in mind but there are ambiguities. Interview them to convert unknowns into decisions before any code is written.

Topic: $ARGUMENTS

## Rules

- **One question at a time.** Ask, wait for the answer, let it shape the next question. Never dump a questionnaire.
- **Prioritize by blast radius.** Ask first the questions whose answers would change the architecture — data models, type interfaces, external contracts, anything user-facing. Cosmetic and mechanical questions come last or not at all.
- **Prefer options over open prompts.** Where the codebase or common practice suggests 2-4 plausible answers, present them (use AskUserQuestion when available) with a recommendation and the trade-off in one line each. The user recognizing the right answer is faster than composing it — this is how you mine their unknown knowns.
- **Do your homework between questions.** If a question can be answered by reading the code instead of asking, read the code and don't ask. Only spend the user's attention on genuine decisions.
- **Know when to stop.** Stop when the remaining unknowns wouldn't change the architecture — say so explicitly, and note that the rest can be improvised during implementation.

## Deliverable

End with a short brief: the decisions made (with the user's answers), the deliberately-open questions and the conservative default you'll use for each, and a suggested implementation order that front-loads the parts most likely to change (data models, interfaces, user-facing behavior) and leaves mechanical refactoring for last. This brief should be pasteable as the prompt for the implementation session.
