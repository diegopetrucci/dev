---
header:
  image: /assets/posts/cutting-tokens.png
  image_height: 420px
  image_position: center
  og_image: /assets/posts/cutting-tokens.png
layout: single
title: What’s new in the last harness — August 2026
---

A lot has changed in the latest versions of [the last harness](https://github.com/diegopetrucci/the-last-harness), my best take on what an AI coding harness should look like.

### Token usage has been massively cut down

A lot of the work has focused on cutting token waste and reducing errors and tooling issues. The results from my own usage are promising: token consumption is down ~18%. That percentage is made up, but it reflects how the change feels day to day.

The main culprit was pi-subagents. TLH used to use [nicobailon’s version](https://github.com/nicobailon/pi-subagents), with just a few additions of its own. That project is brilliant, but it has grown very complex, and its schemas exposed a lot of unnecessary tooling to the main agent. This polluted the context and burned tokens for no real gain.

TLH now embeds its own very, very trimmed-down version, tailored to what it actually uses.

I’ve started similar work on every other dependency. I’ve also completely removed [RTK](https://github.com/rtk-ai/rtk), [which seems to cause more token waste than gain](https://www.stet.sh/blog/gpt-56-token-saving-modes), and the [FFF search](https://github.com/ShpetimA/pi-fff). Pi extension makers: be very mindful of what your work ships!

### Reliability

The pi-subagents library had grown beyond what TLH needed, and cracks were starting to show. I noticed more and more failures while subagents like the developer and librarian were running. Nothing catastrophic, but enough to burn tokens and subscription quota and slow development down.

The architect, TLH’s primary agent, now checks in on subagents more often. Hard timeouts have dropped as a result, because it can steer their work and keep an eye on them.

In practice, subagents now mostly work asynchronously. Refined prompts and new soft timeouts help them wrap up earlier and more concisely.

This has also reduced the `cache miss` warnings recently introduced by [`pi`](https://pi.dev).

### Subagents UX tweaks

Subagents now show which ticket they’re analysing or working on (especially the developer!), the TUI is less cluttered, and it’s clearer when one is stuck or just “thinking”.

### Herdr and Cmux support

TLH now correctly sends its working status to both [Herdr](https://herdr.dev) and [Cmux](https://cmux.com). Before, TLH was shown as working only when the architect was doing something; now, subagents’ work is tracked too. By the way, give both a try—they’re great: Herdr on your always-on machine, Cmux locally.

## What’s next for TLH

In the short term, I want TLH to become leaner, more reliable, and a little more customisable. The next few releases will focus on those goals. I want TLH to work for everyone who buys into its philosophy, and I don’t think we’re there yet.

In the longer term, I’ve noticed a pattern in my own usage: I no longer spawn a gazillion sessions for different pieces of work. Instead, I tend to use one long-lived session with a high-level view of everything that’s going on.

Improvements in model compaction have made this possible, but there’s still UX work to do, and I don’t think any of the major harnesses have quite nailed it yet. I have some ideas, and hopefully I’ll have more to share soon.
