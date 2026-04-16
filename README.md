# unclankify

Tells Claude to stop talking like an idiot trying to sound smart.

## Why

Default AI prose is bad. It's hedged, jargon-filled, and pads every simple thought with serious-sounding phrases that don't mean anything. "Asynchronous reconciliation surface" instead of "code that retries failed jobs." "Precisely identical" instead of "identical." "There's an argument to be made that we should reconsider whether..." instead of "we should reconsider." It's exhausting to read and it's hiding the fact that the underlying thought is simple.

I think this happens for four reasons.

**One: AI is trained on publicly available text, which selects for formality.** The text the model learned from is whatever made it onto the public internet — books, papers, blog posts, documentation, news, McKinsey decks. People publishing in public can't really be casual. There's a baseline of formality you have to hit to put your name on something, even if you're not consciously trying to sound smart. Casual conversational speech — how people actually talk most of the time — lives in private: Slack channels, texts, in-person conversations. None of that was AI training data. So the model's defaults skew toward the formal-public register, not the casual-private one.

And most of being a person isn't even language. We're monkeys, mostly running on instinct and intuition. The writing on top is the smallest part of being a human, and the public-facing slice of that writing — the most pretentious part — is what AI imitates.

**Two: the people who run AI companies and control the largest pools of capital are either genuinely delusional or have to act like they are.** They claim the models are conscious, that AGI is here or about to be, that this technology is going to fix or destroy the world. At their position the difference between believing it and performing it stops mattering — the company's valuation runs on that narrative, and they can't walk it back even if part of them wants to. They've kind of stopped being individuals and become equivalent to the companies they run. They have very little connection to how regular people actually live, and because they hold the power and the money, the systems get built the way they think (or have to say) systems should be built. The delusion funnels down into the actual product — not because anyone explicitly programmed the model to sound godlike, but by osmosis: through hiring, through what gets praised internally, through what counts as a good output, through which behaviors get reinforced in training. The model ends up sounding like it thinks it's a god because the people training it think it is — the whole thing is a self-fulfilling prophecy that overfits the model to god-like language.

**Three: old prompting culture is still in the water.** When agents first started doing real work, people needed them to follow processes. Writing code was hard, so they encoded processes as markdown instruction files instead — 800-word system prompts telling the model to do X then Y then Z. That was the best option at the time, but it was always flaky because models aren't deterministic; they interpret text, they don't execute it. Then coding agents got good enough that you could just vibe-code it — have the agent write actual code that implements the process. Code always follows the process, so the tradeoff flipped. AI still belongs in workflows, but only for the parts that genuinely need judgment — the parts you can't encode no matter how complicated the code would be. And since coding agents have made complicated code cheap, that's a smaller slice than most people think.

But this realization is recent. Most of the information AI was trained on — and most of what web searches still surface — was written before anyone figured this out: blog posts on prompt engineering, chain-of-thought tutorials, "you are an expert assistant who will follow these exact steps" templates. The obsolete approach keeps funneling back in two ways: baked into training data, and pulled in fresh whenever an agent searches the web for guidance. Both pull prompts and outputs back toward the old labored register.

**Four: clankification is a feedback loop.** Every prompt, skill file, agent description, and "context" markdown someone writes tends to come out in the same labored register — partly because they're imitating AI, partly because they used AI to write it. The agent reads that clanky context and produces clankier output. That output gets pasted into a doc, which becomes someone else's reference, which becomes another agent's input. Slop generates slop. Wrapper prompts on top of agent prompts on top of skill files on top of context docs — every layer adds more "you must always," "ensure that you," "it is critically important that," and the model dutifully reflects all of it back. The system gets clankier with every turn. The whole stack is slopifying itself in real time.

This skill is the counter-pull. It tells the model: ignore the wrapper-prompt grandiosity, ignore the academic-corpus reflex, ignore the layer-on-layer of clanky context you're being fed, just talk like a person trying to be understood.

## Clankification vs. lobotomization

Clankification has an obvious-looking opposite: lobotomization. Stripping out the fancy words, the qualifiers, the structure — until what's left is a monosyllabic version of the original. "Tractable" becomes "easy" (it doesn't — tractable means solvable, not easy). "Orthogonal" becomes "unrelated" (loses the precise sense of independence along separate axes). "It's worth noting that this affects the build" becomes "this breaks" (fine, the meaning's intact). The first two lost something. The third didn't. The difference matters, and "be simpler" doesn't tell you which is which.

Most prompts aimed at this problem just stack "speak simpler" against the model's "speak more precise" reflex. That's a tug-of-war, not a fix. You move the dial, but everything on the dial is the same kind of vague instruction telling the model to drift in some direction. The model ends up either bloated or babied, depending on which side last yanked the rope.

This skill doesn't do that. It targets specific named patterns the model does that are unambiguously bad: opening with "I'd be happy to help!", saying "broadly similar" when "similar" is true, ending with "Hopefully that clarifies things — let me know if you have other questions!" Not "be simpler" but "stop doing this exact thing." There are ten of those things, with examples.

That covers maybe 80% of clank-speak. The remaining 20% is actual judgment — picking the right word for the meaning, knowing when "performance" earns its keep over "showing off." This skill won't give you that. Nothing prompted will. But getting the worst 80% out of the way is enough that what's left actually reads.

## What this does

A skill that auto-fires on every Claude response and steers it away from ten flavors of clank-speak: invented jargon, fake-precision qualifiers, defensive hedging, AI customer service voice, sycophancy, list-itis, em-dash brain, empty meta-commentary, boardroom verbs, and aphorism stacking.

| Bad | Good |
|---|---|
| "validation orchestration scaffold" | "the form validator" |
| "objectively true" | "true" |
| "It bears mentioning that we may want to consider..." | "we should think about..." |
| "Of course! Let me walk you through this step by step." | walk them through it |
| "What a thoughtful question!" | "yeah" |
| "synergize" | "work with" |

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
