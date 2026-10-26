# clear-explainer

Make technical topics easier to understand. **clear-explainer** is an Agent Skill that gives coding agents a clear, conversational explanation style, similar to what people often appreciate in ChatGPT.

It leads with the answer, uses plain language and short sections, adds an everyday analogy when it helps, and skips filler. It works for questions, code, errors, comparisons, and other requests where the user wants to understand something.

## What it does

- Answers the question directly before adding detail.
- Explains unfamiliar ideas in plain language, at the reader's level.
- Uses examples and everyday analogies where they make an idea easier to picture.
- Adapts to follow-ups such as “make it simpler” or “go deeper.”
- Keeps task requests focused on the task and applies the style to the explanation.

## Install

Install from the skills directory:

```bash
npx skills add poulvinay/clear-explainer
```

Or install manually for Claude Code:

```bash
mkdir -p ~/.claude/skills/clear-explainer
curl -o ~/.claude/skills/clear-explainer/SKILL.md \
  https://raw.githubusercontent.com/poulvinay/clear-explainer/main/SKILL.md
```

Skills-compatible agents discover the skill from its `SKILL.md` file. Restart your agent if it does not appear right away.

## Usage

Ask the agent to explain a topic, or use a prompt such as:

- “What does idempotent mean?”
- “Explain this error in simpler terms.”
- “What's the difference between a process and a thread?”
- “I still don't get it. Can you explain it another way?”

The skill also applies to the explanatory part of a task, such as fixing a bug or changing code; it does not replace doing the requested task.

## Example

**Question:** “What does a 404 mean?”

**Answer:** A 404 means the server is working, but the page could not be found at that address. The page may have moved, been deleted, or the URL may be mistyped.

More examples are in [`examples/worked-examples.md`](examples/worked-examples.md).

## How it works

The skill's instructions live in [`SKILL.md`](SKILL.md). It defines when to use the explanation style and how to keep answers direct, readable, and accurate. The prompt examples used to evaluate the skill are in [`evals/evals.json`](evals/evals.json).

For Claude Code users, [`hooks.json`](hooks.json) includes an optional `UserPromptSubmit` hook that reminds Claude to use the skill when a prompt contains a question mark. The hook requires `jq` and must be added to `~/.claude/settings.json`; it is not needed for other agents.

## Contributing

Issues and pull requests are welcome. Useful contributions include clearer examples, better coverage for different kinds of questions, and improvements to when the skill should or should not apply.

## Suggested GitHub topics

Add these topics in the repository settings for discoverability:

`agent-skills` · `ai-agents` · `claude-code` · `developer-tools` · `plain-language` · `explain` · `prompt-engineering`
