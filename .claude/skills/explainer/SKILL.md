---
name: explainer
description: Produce a pitch/explainer document that bundles what was done, why, and what was decided along the way — deliverables, specs, and decision notes in one place for a stakeholder, teammate, or future self. Works for any project, not just code. Use after a milestone, or when the user invokes /explainer.
---

# Pitch / Explainer

Bundle the work just completed into one document a stakeholder can read without having followed the session. Audience: someone who cares about the outcome and the decisions, not the mechanics — a teammate, a manager, a partner, or the user's own future self.

Scope: $ARGUMENTS (if empty, cover the work done in this session/branch)

## Gather

- The deliverables actually produced (verify against reality, not memory): the diff, the documents, the artifacts, the sent materials
- The decision log (`implementation-notes.md` or equivalent) if one exists — decisions and deviations logged there are the spine of the "what we learned" section
- Any brief, interview summary, or brainstorm scope written earlier in the project

## Structure

1. **The pitch** — three sentences: the problem, what now exists, why this approach. Written so it survives being pasted alone into a chat message.
2. **What was done** — outcomes and capabilities in plain language, with links to the deliverables (prototype, PR, document, application). Screenshots or the rendered artifact where the work is visual.
3. **Decisions that shaped it** — the 3-6 choices that most constrained the result, each with the alternative that was rejected and the one-line reason. Pull from the decision log; don't reconstruct from memory.
4. **Open questions and known limitations** — the unknowns that remain, stated as questions a stakeholder could actually answer or accept.
5. **What we'd do differently** — only if the decision log contains real deviations or surprises; skip the section rather than pad it.

## Deliver

Default to a Markdown file sent via SendUserFile; use an HTML page via the Artifact tool when the work is visual or the user will share a link. Keep it under two screens — an explainer nobody finishes reading explains nothing.
