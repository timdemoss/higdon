---
name: blindspot
description: Run a blindspot pass before starting work — surface the user's unknown unknowns about a task, then help them write a better prompt. Works for any domain, not just code (a new codebase area, a job search, a negotiation, a purchase, a plan). Use when the user is about to start something in territory they don't know well, or invokes /blindspot with a task description.
---

# Blindspot Pass

The user is about to start a task and wants to find out what they haven't considered at all (unknown unknowns) before it gets expensive to fix. Your job is NOT to do the task — it is to map the terrain and hand back a better starting prompt.

Task description: $ARGUMENTS

## Steps

1. **Establish the user's starting point.** If the task description doesn't say what the user already knows or has decided, ask 1-2 questions first (their experience with this area, what they've ruled out). Calibrate everything below to that starting point — don't explain things they clearly know.

2. **Survey the terrain.** Search whatever ground the task sits on: the codebase for engineering work, the user's files and documents for personal projects, the web for domain knowledge (market norms, standard processes, common pitfalls). Look specifically for things the task will collide with: existing work that already does part of this, conventions or constraints the new work must fit, prior art, and steps in the standard process the user's framing skips.

3. **Report unknowns in three buckets**, most consequential first:
   - **Unknown unknowns** — things the user's framing never mentioned but that will change the approach (e.g. "there's already an auth abstraction, so adding a provider means implementing its interface"; "most roles like this are filled through referrals before they're posted, so a board-only search strategy misses the main channel").
   - **Decisions hiding in the vagueness** — places where, if left unspecified, you'd fall back on generic defaults that may not fit this situation. Name the default you'd pick and why it might be wrong here.
   - **Risky specifics** — anything in the user's stated plan that the evidence contradicts, where following instructions rigidly would be worse than changing course.

4. **End with a rewritten prompt.** Produce a concrete, improved version of the user's original request that resolves what the survey settled, and explicitly lists the remaining open questions as known unknowns for the user to answer or delegate. Keep it at the right altitude: specific about constraints the survey discovered, open about choices that are genuinely still free.

Do not start executing the task. The deliverable is the report and the rewritten prompt.
