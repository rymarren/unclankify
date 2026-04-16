---
name: unclankify-repo
description: Use when the user wants to clean up or unclankify the AI/agent context files in a repository — CLAUDE.md, AGENTS.md, skill files, agent prompts, slash commands, etc.
---

# Unclankify the whole repo

The user wants you to find every AI-facing markdown file in the repo and rewrite each one in plain English, applying the `unclankify` skill's principles. This fights the feedback loop where clanky context produces clankier output, which becomes someone else's clanky context.

## What counts as an AI file

Look for these:

- `CLAUDE.md`, `AGENTS.md`, `GEMINI.md` (anywhere in the tree)
- `.cursorrules`, `.windsurfrules`, `.aider.conf.yml`
- `.github/copilot-instructions.md`
- `**/skills/**/SKILL.md` and `**/skills/**/*.md`
- `.claude/commands/**/*.md` and `commands/**/*.md`
- `.claude/agents/**/*.md` and `agents/**/*.md`
- `prompts/**/*.md` and `system_prompts/**/*.md`
- Anything else whose path or filename suggests it's an agent prompt, tool description, or model instruction

Don't touch:

- `README.md` and other docs primarily for humans (unless the user explicitly asks)
- Code files — only the markdown layer holds AI prose
- License files, changelogs, contribution guides
- `node_modules`, `vendor`, `.git`, build artifacts

## How to do it

1. Find candidates with Glob or Grep. Don't dump the whole tree.
2. List the files for the user. Confirm before doing anything destructive.
3. For each file, in batches the user can review:
   - Read it.
   - Decide if it's actually clanky. If it's already plain, skip and say so.
   - Rewrite it, applying every principle from the `unclankify` skill.
   - Show the diff.
   - Wait for the user to approve THIS file before writing.
4. After each batch, give a one-line summary of what was rewritten and what was skipped.

## What to keep when rewriting

- Factual content: commands, paths, filenames, exact instructions
- Frontmatter fields (`name`, `description`, `type`) — though you can rewrite the description body if it's clanky
- Code blocks — don't touch the code itself
- Real domain vocabulary (`eigenvalue`, `SIGTERM`, `left join`, etc.)

## What to drop

- "You must always," "ensure that you," "it is critically important that"
- Inflated section headers (`## CRITICAL REQUIREMENTS`, `## MANDATORY GUIDELINES`)
- Repeated emphasis (CAPS LOCK words, bold-on-bold, multiple exclamation points)
- Hedge stacks ("may potentially possibly")
- AI customer service voice in instructional prose
- Padding bullets that just rephrase the heading above them

## When to leave something alone

If you're not sure whether weird-looking text is clank or load-bearing, leave it. Someone may have written that instruction because they debugged a specific failure. Ask before smoothing it out.

If a file is structured prompt engineering — a chain-of-thought template, a JSON schema, a structured-output spec, a few-shot example block — don't "make it more natural." That structure is functional, not show.

If a file is short and already plain, say "this one's fine" and move on. Not every file needs rewriting.
