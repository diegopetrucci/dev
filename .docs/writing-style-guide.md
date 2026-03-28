# Writing style guide

Based on the posts currently in [`_posts/`](../_posts/).

## Core voice

- Write in first person.
- Sound like an engineer sharing something that actually worked in practice.
- Prefer pragmatic observations over big claims or theory.
- Keep the tone conversational, but not sloppy.
- A little dry humour is good; overdoing it is not.

## What the writing tends to optimize for

- Start from a real annoyance, limitation, or workflow gap.
- Explain the simpler approach you chose and why.
- Show the concrete artifact: prompt, command, file, screenshot, repo link, commit, or diagram.
- Be explicit about scope: what this post covers, what it skips, and what comes next.
- End with caveats, limitations, or the next step.

## Post structure

This is the default shape to aim for:

1. Open with the problem or tension.
2. Briefly explain why the obvious or existing solution was not good enough.
3. Introduce the setup or approach you actually use.
4. Show the implementation details that matter.
5. Call out limitations, quirks, or tradeoffs.
6. Close with the next step, a follow-up part, or a lightweight invitation for feedback.

## Stylistic habits to keep

- Prefer short paragraphs.
- Use lists when explaining steps, modules, prompt lines, or tradeoffs.
- Use concrete language like "this is what I do", "this covers", "for now", "it works well enough".
- Keep the writing grounded in personal usage rather than pretending to be universal guidance.
- Be comfortable saying when something is messy, incomplete, or still evolving.
- Use links generously when a repo, commit, doc, or tool is part of the explanation.

## Tone guardrails

- Do not sound like marketing copy.
- Do not oversell novelty or certainty.
- Do not make the post read like documentation unless the topic really needs it.
- Do not over-explain basics when the intended reader is likely technical.
- Do not chase perfect completeness; useful slices are better.

## Preferred framing

Good patterns:

- "I ran into this problem..."
- "I prefer this because..."
- "This is good enough for my needs."
- "For now, this covers..."
- "Admittedly, this part is still rough."
- "I like simple stuff."

Avoid overusing:

- Abstract hype about "the future"
- Grand conclusions not backed by your own usage
- Long scene-setting before getting to the actual setup

## Editing notes

- Keep proper nouns and product names consistent.
- Trim sentences that stack too many clauses.
- If a sentence contains more than one aside, split it.
- Keep jokes light and quick.
- If a post includes code or prompts, prefer the exact snippet over paraphrasing it.

## Quick checklist

Before publishing, check that the post:

- Starts from a concrete problem
- Shows the actual thing you used or built
- States the scope clearly
- Includes at least one practical takeaway
- Mentions tradeoffs or limitations
- Sounds like you, not like generic AI tooling content

## Reusable template

```markdown
## The problem

What was annoying, expensive, brittle, distracting, or overcomplicated?

## What I wanted instead

What constraints mattered? Simplicity, local-first, low babysitting, clear boundaries, etc.

## The setup

Show the actual command, prompt, file, architecture slice, or workflow.

## Why this approach

Why this instead of the more obvious alternative?

## Limitations / quirks

What is still rough, temporary, or incomplete?

## What comes next

What would you improve, automate, or cover in a follow-up?
```
