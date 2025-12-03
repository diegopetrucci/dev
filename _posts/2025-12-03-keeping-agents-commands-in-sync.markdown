---
layout: single
title:  "Keeping global commands for CLI agents in sync"
date:   2025-12-03 10:00:00 +0100
categories: agents llm ai claudecode cli codex gemini amp opencode cursor
---

Lately, I've found myself in this predictament:

1. I write a lot of code using CLI agents
2. I switch often between them as none has a particularly strong moat
3. I have a set of global, custom, commands that I like to use across projects

Hence, I need to have a way to keep them in sync. I've solved syncing my setup across different machines by using dotfiles and chezmoi, but, so far, I had no real solution for keeping the commands themselves in sync.

After some research, I've more or less collected all the places where these agents store their configs:

- Amp: `~/.config/amp/commands`
- Claude: `~/.claude/commands`
- Codex: `~/.codex/prompts`
- Cursor: `~/.cursor/commands`
- Gemini: `~/.gemini/commands`
- Opencode: `~/.config/opencode/command`

To make my life easier, [I've also created a custom command](https://github.com/diegopetrucci/dot/blob/main/.codex/prompts/sync-global-agents-commands.md) that I run once in a while to keep them all updated:

```markdown
Check each of these directories:

~/.codex/prompts
~/.claude/commands
~/.cursor/commands
~/.config/opencode/command
~/.config/amp/commands
~/.gemini/commands

If any of them contains an md that the others do not, or a newer version, sync it to the other directories too.
```

It works well enough for my needs. Oh, and in case you're curious, [these are my dotfiles](https://github.com/diegopetrucci/dot/).
