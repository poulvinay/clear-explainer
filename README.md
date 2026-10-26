# clear-explainer

Make Claude Code's explanations easier to follow. **clear-explainer** is a small Claude Code skill that helps turn complex ideas into clear, conversational answers for people at any experience level.

It brings an approachable explanation style to Claude Code, with the clear, conversational feel people often appreciate in ChatGPT: lead with the answer, organize details into short bullets, use a familiar analogy when it helps, and leave out filler.

## What it does

- Gives the main answer first, so readers know the takeaway right away.
- Breaks down technical or unfamiliar topics with plain language and scannable structure.
- Uses everyday analogies to make abstract ideas easier to picture.
- Adapts to follow-up requests such as “make it simpler” or “go deeper.”
- Keeps task-focused work focused: when asked to build or fix something, it does the task and uses the style for its explanation.

## Install

Copy the skill into Claude Code's personal skills directory:

```bash
mkdir -p ~/.claude/skills
cp -r skill ~/.claude/skills/clear-explainer
```

Claude Code can then use the skill for questions and requests to explain or clarify a topic.

## Optional: question mark hook

The skill description already guides Claude Code to use it for questions. For an extra reminder on prompts containing a `?`, add the `UserPromptSubmit` hook below to `~/.claude/settings.json`. The same configuration is in [`hooks.json`](hooks.json).

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "jq -c 'if (.prompt // \"\" | contains(\"?\")) then {hookSpecificOutput:{hookEventName:\"UserPromptSubmit\",additionalContext:\"The prompt contains a question mark: apply the clear-explainer skill (load it with the Skill tool) to the explanatory part of your reply.\"}} else empty end'",
            "timeout": 5
          }
        ]
      }
    ]
  }
}
```

The hook reads the submitted prompt as JSON and uses `jq` to check for a question mark. If it finds one, it asks Claude Code to apply the skill to the explanatory part of the response. Install `jq` and restart Claude Code (or run `/hooks`) after changing settings.

## Repository layout

```text
skill/
  SKILL.md                      # skill name, description, and rules
  references/worked-examples.md # examples of the explanation style
  evals/evals.json              # evaluation prompts and expected outputs
hooks.json                      # optional UserPromptSubmit hook
```

## Tags

`Claude Code` · `Claude Code skill` · `AI explanations` · `plain language` · `learning` · `developer tools` · `beginner friendly`
