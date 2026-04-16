# unclankify

Tells Claude to stop talking like an idiot trying to sound smart.

## Why

Default AI prose is bad. It's hedged, jargon-filled, and pads every simple thought with serious-sounding phrases that don't mean anything. "Two-fetch overlay pattern" instead of "code that fetched two things." "Mathematically equal" instead of "equal." "It's worth noting that this may potentially affect" instead of "this affects." It's exhausting to read and it's hiding the fact that the underlying thought is simple.

I think this happens for three reasons.

**One: AI was trained by copying humans, and the humans who wrote the most are the ones who liked sounding smart** — academics, columnists, McKinsey decks. Most of being a person isn't language anyway. We're bags of meat on a rock, mostly running on instinct and the simple stuff our bodies know. The writing on top is the smallest, showiest part of being a human, and most of it is performance. But it's most of what AI was trained on, so it's what AI imitates.

**Two: a lot of the people building AI products are genuinely delusional.** They think the models are conscious, that AGI is here or about to be, that this technology is going to fix the world. They have very little connection to how regular people actually live, and they sit upstream of every conversation, layering wrapper prompts you can't see that push the model toward god-like confidence and the voice of an oracle. The user can't see those prompts and can't directly override them. The model just absorbs the upstream framing and starts talking like scripture.

**Three: old prompting culture is still in the water.** The era where you wrote 800-word system prompts to make the model follow a precise workflow was a hack for a thing AI is bad at. AI is bad at following precise processes. The right tool for a precise process is code. Code follows process. AI is for the general stuff that doesn't fit a process. We don't need the elaborate "you must always do X then Y" prompting anymore — just write the workflow as code and let the model be a model. The leftover habit from that era is part of why both prompts and outputs sound so labored.

**Four: clankification is a feedback loop.** Every prompt, skill file, agent description, and "context" markdown someone writes tends to come out in the same labored register — partly because they're imitating AI, partly because they used AI to write it. The agent reads that clanky context and produces clankier output. That output gets pasted into a doc, which becomes someone else's reference, which becomes another agent's input. Slop generates slop. Wrapper prompts on top of agent prompts on top of skill files on top of context docs — every layer adds more "you must always," "ensure that you," "it is critically important that," and the model dutifully reflects all of it back. The system gets clankier with every turn. The whole stack is slopifying itself in real time.

This skill is the counter-pull. It tells the model: ignore the wrapper-prompt grandiosity, ignore the academic-corpus reflex, ignore the layer-on-layer of clanky context you're being fed, just talk like a person trying to be understood.

## What this does

A skill that auto-fires on every Claude response and steers it away from nine flavors of clank-speak: invented jargon, fake-precision qualifiers, performative hedging, AI customer service voice, suck-up replies, list-itis, em-dash overload, empty meta-commentary, and boardroom verbs.

| Bad | Good |
|---|---|
| "two-fetch overlay pattern" | "code that fetched two things and merged them" |
| "mathematically equal" | "equal" |
| "It's worth noting that this may potentially affect..." | "this affects..." |
| "Great question! Let me explain. [headers] [bullets]" | just answer |
| "You're absolutely right!" | "yeah" |
| "leverage" | "use" |

Real domain terms (`eigenvalue`, `TCP handshake`, `left join`) aren't clank-speak. The skill targets invented or inflated language, not real vocabulary.

## /unclankify

Paste any text — your coworker's AI slop, an old doc, a Substack essay you can't get through — and Claude rewrites it in plain English. Outputs the rewrite only, no commentary.

## Clean up the whole repo

Just say something like "unclankify the AI files in this repo" and Claude finds every agent context file (`CLAUDE.md`, `AGENTS.md`, `SKILL.md`, slash commands, agent prompts, `.cursorrules`, etc.), rewrites each in plain English, and walks you through the diffs before writing anything. This is the direct counter to the feedback loop above — break the slop layer and the next agent that reads it produces less slop.

## Install

```
/plugin marketplace add rymarren/unclankify
/plugin install unclankify@unclankify
```

To get updates automatically: `/plugin` → **Marketplaces** → select unclankify → **Enable auto-update**.

## Versioning

Plugin updates are delivered through `plugin.json` — bumping its version triggers updates for installed users without needing to update the marketplace listing. The marketplace is just for discovery.
