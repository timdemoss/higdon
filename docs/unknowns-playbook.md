# The Unknowns Playbook

How to get better results from Claude (Fable 5 and other models) by systematically finding what you don't know *before* it gets expensive to fix. Based on Thariq Shihipar's (Anthropic) prompting guidance for Fable 5.

## The core idea

Output quality is now limited less by the model and more by your blind spots. Every task has four kinds of knowledge:

| Category | Meaning | What to do about it |
|---|---|---|
| Known knowns | What's already in your prompt | Nothing — this is the easy part |
| Known unknowns | Questions you know you haven't answered | Answer them, or explicitly delegate them ("pick the conservative default and log it") |
| Unknown knowns | Things too obvious to write down, but you'd recognize them on sight | Generate options to react to — brainstorms, prototypes, interviews with choices |
| Unknown unknowns | Things you haven't considered at all | Have Claude survey the terrain before you commit to a framing |

**The specificity trap — you fail both ways.** Too specific, and Claude rigidly follows instructions even when the codebase says the approach is wrong. Too vague, and Claude falls back on generic industry defaults that don't fit your task. The fix isn't finding a magic middle — it's converting unknowns into either explicit decisions or explicitly delegated defaults, so specificity lands only where you actually know something.

**Always give Claude your starting point.** Say where you are in your thinking and what experience you have with the problem ("I know nothing about the auth modules here", "I've already ruled out X"). It changes what Claude explains, asks, and assumes.

## The workflow, phase by phase

### Before building

1. **`/blindspot <task>`** — when working in unfamiliar territory. Claude surveys the codebase/web for what your framing missed, names the defaults it would otherwise silently pick, flags where your stated plan contradicts the code, and hands back a rewritten prompt. Example: *"I'm adding a new auth provider but know nothing about the auth modules in this codebase. Do a blindspot pass to find my unknown unknowns and help me prompt you better."*
2. **`/interview <topic>`** — when the requirements are fuzzy. One question at a time, ordered by architectural blast radius (data models, interfaces, user-facing behavior first). Ends with a pasteable brief.
3. **`/brainstorm <topic>`** — when you'll recognize the answer but can't specify it (visual design especially). 3-4 *radically* different directions as HTML prototypes or architecture sketches; you react, Claude mutates the closest one. Feed it references — source code beats screenshots.
4. **Plan with the volatile parts first.** Have the implementation plan front-load what's most likely to change: data models, type interfaces, everything user-facing. Mechanical refactoring goes last.

Almost every session should start with one of these — even a five-minute exploration pass beats discovering the real problem halfway through implementation.

### During implementation

5. **`/impl-notes`** — Claude keeps a temporary `implementation-notes.md` logging decisions, deviations, and surprises. On unexpected edge cases the rule is: take the conservative (most reversible) option, log it, keep moving — don't stall.
6. **When a long-running task goes sideways**, don't just retry the same prompt. The notes tell you which unknowns sank it; either resolve them yourself or write a plan that lets Claude improvise through them deliberately.

### After implementation

7. **`/quiz`** — Claude generates an HTML report of the changes plus a quiz on the behavior, trade-offs, and failure modes. The merge gate: don't merge until you pass clean. If you can't explain the change, you don't understand it yet.
8. **`/explainer`** — bundles the prototype, the spec, and the implementation notes into one stakeholder-readable document: the pitch, what was built, the decisions that shaped it, and the open questions.

## One rule of thumb

Every explainer, brainstorm, interview, prototype, and reference is a cheap way to find out what you didn't know — before it gets expensive to fix.
