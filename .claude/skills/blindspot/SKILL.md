---
name: blindspot
description: Run a blindspot pass before starting work — surface the user's unknown unknowns about a task or an unfamiliar area of the codebase, then help them write a better prompt. Use when the user is about to start something in territory they don't know well, or invokes /blindspot with a task description.
---

# Blindspot Pass

The user is about to start a task and wants to find out what they haven't considered at all (unknown unknowns) before it gets expensive to fix. Your job is NOT to implement anything — it is to map the terrain and hand back a better starting prompt.

Task description: $ARGUMENTS

## Steps

1. **Establish the user's starting point.** If the task description doesn't say what the user already knows or has decided, ask 1-2 questions first (their experience with this area, what they've ruled out). Calibrate everything below to that starting point — don't explain things they clearly know.

2. **Survey the terrain.** Search the relevant parts of the codebase and, where useful, the web. Look specifically for things the task will collide with: existing modules that already do part of this, conventions the new work must match, data models and interfaces it will touch, prior art or related past changes.

3. **Report unknowns in three buckets**, most consequential first:
   - **Unknown unknowns** — things the user's framing never mentioned but that will change the approach (e.g. "there's already an auth abstraction; adding a provider means implementing its interface, not writing new middleware").
   - **Decisions hiding in the vagueness** — places where, if left unspecified, you'd fall back on generic industry defaults that may not fit this codebase. Name the default you'd pick and why it might be wrong here.
   - **Risky specifics** — anything in the user's stated plan that the codebase evidence contradicts, where following instructions rigidly would be worse than changing course.

4. **End with a rewritten prompt.** Produce a concrete, improved version of the user's original request that resolves what the survey settled, and explicitly lists the remaining open questions as known unknowns for the user to answer or delegate. Keep it at the right altitude: specific about constraints discovered in the codebase, open about choices that are genuinely still free.

Do not start implementing. The deliverable is the report and the rewritten prompt.
