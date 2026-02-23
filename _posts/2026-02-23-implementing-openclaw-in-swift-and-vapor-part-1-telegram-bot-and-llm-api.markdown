---
header:
  image: /assets/reimplementing-openclaw/part-one-openclaw-swift.png
  og_image: /assets/reimplementing-openclaw/part-one-openclaw-swift.png
layout: single
title:  "Implementing OpenClaw in Swift and Vapor, part 1: telegram bot & Anthropic APIs"
date:   2026-02-23 10:00:00 +0100
categories: agents llm ai swift vapor telegram anthropic
---

A lot (!) of people are talking about OpenClaw, but not many seem to know how it actually works under the hood.

Its core components, however, are surprisingly simple — and I think trying to reimplement it could be a good introduction for engineers to these new systems, as you end up learning a lot about orchestration, tool execution boundaries & safety, and where model prompts stop and system design starts.

Hence, I have been building my own version in Swift, using Vapor for the backend: [diegopetrucci/claudio](https://github.com/diegopetrucci/claudio/). The project is loosely based on this write-up by Dabit: [How OpenClaw works](https://gist.github.com/dabit3/bc60d3bea0b02927995cd9bf53c3db32).

I am also building this in a compartmentalized way so that, at (almost) any point, it can be run locally as a usable slice of the final system. I prefer this over trying to wire everything at once and only getting value at the end.

With that out of the way, let's talk about the first tranche of changes:

1. Setting up the Telegram bot interface
2. Interfacing with Anthropic's API from the Vapor backend

Scope-wise, this covers the code from the very first commit [up to being able to send messages](https://github.com/diegopetrucci/claudio/tree/df2c8d55dd20613ef8bc3c277e3b545d677b359f). That link lets you browse the repo at that exact moment in time.

As a note, I won't cover how to set up Vapor. I'm not an expert, and [their docs are great](https://docs.vapor.codes/).

### Telegram and Anthropic API prep

Go to Telegram, chat with the [BotFather](https://telegram.me/BotFather) bot, and create your own. Write your ID in Vapor's `.env`, make sure it's ignored by git, and completely forget about it.

Do the same for Anthropic's API key.

We are also using the [SwiftAnthropic library](https://github.com/jamesrochabrun/SwiftAnthropic) to talk with Anthropic's API.

### Our starting point

Before adding memory, tools, or any autonomous loops, we want the minimum end-to-end path:

- Send the bot a message
- Receive a reply

We are not concerned yet with any state persistence — each message will be a brand new "conversation:

![Telegram chat showing per-message amnesia]({{ site.baseurl }}/assets/reimplementing-openclaw/amnesia-convo.png)

### The modules

The project is structured in a few Swift packages, and please note that we will ignore Docker for now:

![Architecture diagram]({{ site.baseurl }}/assets/reimplementing-openclaw/part-one-modules-diagram.png)

The architecture is quite simple:

- **AnthropicClient**: sets up the `Anthropic` API call, sends it the user message, and receives a reply
- **TelegramClient**: thin wrapper around Telegram's `sendMessage` and `getUpdates` APIs
- **TelegramBotService**: orchestrates bot behavior for incoming text: takes a Telegram message, asks Anthropic for a reply, then sends that reply back to Telegram
- **TelegramPollingLifecycleHandler**: where more of the magic lives, as it runs the long-polling loop as a Vapor lifecycle component. It continuously fetches updates from Telegram, filters/processes valid user text messages, invokes the bot service handler, and handles retry/cancellation/shutdown

Admittedly, `TelegramPollingLifecycleHandler` is already doing too much, but we will deal with that in the future.

## What comes next

Memory! As mentioned, the bot at the moment has per-message amnesia, as it has no concept of a history or previous messages.

As a reminder, if you want to follow along, the code is in [diegopetrucci/claudio](https://github.com/diegopetrucci/claudio/) and this post's scope ends at commit [`df2c8d55dd20613ef8bc3c277e3b545d677b359f`](https://github.com/diegopetrucci/claudio/commit/df2c8d55dd20613ef8bc3c277e3b545d677b359f).

I did not start the project thinking of writing about it, so the first few commits are not semantically marked (the subsequent ones all have a prefix). But I'm sure you'll get the gist.
