---
name: interview
description: Structured interview to turn a fuzzy idea into an actionable spec — ask the user one question at a time, prioritized by how much the answer changes the shape of the work. Works for any domain (a feature, a job search, a trip, a document, an event). Use when the user has a goal in mind but hasn't pinned down the requirements, or invokes /interview.
---

# Structured Interview

The user has a goal in mind but there are ambiguities. Interview them to convert unknowns into decisions before the real work starts.

Topic: $ARGUMENTS

## Rules

- **One question at a time.** Ask, wait for the answer, let it shape the next question. Never dump a questionnaire.
- **Prioritize by blast radius.** Ask first the questions whose answers would change the shape of everything downstream — for code that's data models, interfaces, and user-facing behavior; for a job search it's target role, location/remote, and salary floor; for a document it's audience and desired outcome. Cosmetic questions come last or not at all.
- **Prefer options over open prompts.** Where the evidence suggests 2-4 plausible answers, present them (use AskUserQuestion when available) with a recommendation and the trade-off in one line each. The user recognizing the right answer is faster than composing it — this is how you mine their unknown knowns.
- **Do your homework between questions.** If a question can be answered from the user's files, the codebase, or a quick search, answer it yourself and don't ask. Only spend the user's attention on genuine preferences and decisions.
- **Know when to stop.** Stop when the remaining unknowns wouldn't change the overall shape of the work — say so explicitly, and note that the rest can be improvised during execution.

## Deliverable

End with a short brief: the decisions made (with the user's answers), the deliberately-open questions and the conservative default you'll use for each, and a suggested order of work that front-loads the parts most likely to change and leaves mechanical work for last. This brief should be pasteable as the prompt for the execution session.
