---
header:
  image: /assets/self-improving-agents-header.png
  og_image: /assets/self-improving-agents-header.png
layout: single
title:  "A simple way to add memory to agents and make them self-improve"
date:   2026-02-10 08:00:00 +0100
categories: agents llm ai self-improvement
---

LLM agents are great, but them not having memory and not "learning on the job" is less than ideal. Take `AGENTS.md`, a hack borne out this need.

These days there's quite a lot of discourse on X about ways to improve this flow, and to make agents learn automatically. People have come up with very complicated setups, but I like simple stuff (maybe a skill issue, who knows). This is what I got so far:

1. For each project, I add a short section to `AGENTS.md` that tells the agent to keep a private notes file (`.agents/notes.md`) and update it every time it learns something new, I correct it, or it finds that something is wrong.
2. Each note line starts with a counter, starting at `[0]`.
3. Before writing a new note, it checks if the idea is already there.
4. If it is, it just increments the counter.
5. When a note reaches `[3]`, it promotes it into the main `AGENTS.md` instructions.

This is all to avoid having to manually edit the agents file for corrections, or having to tell them to do it within conversations.

I use codex primarly, and I've found that it loves to write _a lot_ of notes, which is kind of cute. Plus the file doubles as a nice history of the project.

I've been using this strategy for just a week-ish, so I haven't hit issues with memories being too long; but I assume eventually I'll need to prune them manually, or tell the agents to do it if eg the number of items is > N.

For reference, this is the section in my agents file. It's messy as I wrote it in one go, but it works well enough for now:

```markdown
## Agent notes

- Every time you learn something new, or how to do something in the codebase, if you make a mistake that the user corrects, if you find yourself running commands that are often wrong and have to tweak them: write all of this down in `.agents/notes.md`. This is a file just for you that your user won't read.
- If you're about to write to it, first check if what you're writing (the idea, not 1:1) is already present. If so, increment the counter in the prefix (eg from `[0]` to `[1]`). If it's completely new, prefix it with `[0]`. Once a comment hits the count of `3`, codify it into this AGENTS.md file in the `## Misc` section.
```

Some of the notes it's been taking so far:

```markdown
# Notes

- [0] In this repo environment, Xcode output formatter is `xcsift` (path: `/opt/homebrew/bin/xcsift`), not `xcswift`.
- [0] When moving image detail presentation from `MenubarFeature` internals to `SendItToMyMenuBarApp.swift`, `MenubarImageDetailScreen` must be `public` (including `public init` and `public var body`) because app target imports it from the package module.
- [0] Menubar image detail presentation is now modeled as `Window/window` in `MenubarFeature` (not `Sheet/sheet`) to match macOS window behavior.
- [3] Keep `#if/#endif` directives indented to match the surrounding SwiftUI modifier chain indentation in this repo.
- [2] When running `xcodebuild` commands, if another build is active or `build.db` is locked, retry with exponential backoff starting at 10 seconds, up to 5 attempts.
- [0] In zsh shell snippets, avoid assigning to `status` (read-only); use `rc` or another variable name for exit codes.
- [0] `MenubarScreen.onAppear` is an effective hook for “menu bar opened” behavior in the macOS menu bar app.
- [0] In `MenubarFeature`, AppKit side effects (`NSApplication` activation/termination/window foreground) should be triggered from reducer effects via a dependency provider, not called directly from SwiftUI views.
```

And what it promoted to the `AGENTS.md`:

```markdown
# Misc

- Keep `#if/#endif` directives indented to match the surrounding SwiftUI modifier chain indentation in this repo.
```

That's it. No skills, nor complicated setups.

Give this a try, and please let me know at [@diegopetrucci](https://x.com/diegopetrucci) if you have improvements, if you hate it, or anything else. This is all new for everybody!
