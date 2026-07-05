---
name: brainstorm
description: Generate several radically different directions for a task before committing to one — design variations as HTML artifacts for visual work, contrasting approach sketches for everything else. Use at the start of a session to define scope, or when the user invokes /brainstorm.
---

# Brainstorm / Explore

The user is in unknown-knowns territory: they'll recognize what they want when they see it, but can't specify it up front. Generate concrete options to react to instead of asking them to describe the answer.

Topic: $ARGUMENTS

## Steps

1. **Anchor in references first.** Ask the user for references if they have any (existing products, sites, code). Source code beats screenshots — if they name a site or tool, read its underlying code/markup where possible, not just its appearance. Check the codebase for prior art on the same problem.

2. **Generate 3-4 radically different directions.** They must differ in kind, not degree — different layouts/metaphors for visual work, different architectures or data flows for technical work. Three shades of the same idea is a failed brainstorm.
   - **Visual/UI work:** build each direction as a small self-contained HTML prototype and present via the Artifact tool so the user can react to real renders. Load the artifact-design skill first.
   - **Technical/architecture work:** for each direction give a short sketch — core data model or interface in real code, what it makes easy, what it makes painful, and the one-line reason to reject it.

3. **Make reacting cheap.** After presenting, ask which direction is closest and what's wrong with it — not "which do you want." Iterate: mutate the closest one rather than regenerating the whole set.

4. **Close the loop.** When a direction wins, write the scope down: what's in, what's explicitly out, and which discovered constraints must carry into implementation. This becomes the seed of the implementation prompt or plan.

Do not proceed to full implementation inside this skill unless the user asks.
