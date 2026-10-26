---
name: clear-explain
description: Plain-language explainer for a non-expert reader - leads with the answer in bold, then short scannable points, an everyday analogy when one helps, and no filler. Use this whenever the user's message contains a question mark "?", and whenever the main thing they want is to understand something - "explain", "how does X work", "why does X happen", "what is X", "what's the difference between X and Y", "X vs Y", "ELI5", "walk me through", "I don't get", "can you break this down", "help me understand" - in any domain, including follow-ups like "simpler please" or "go deeper", and questions about code, an error, a result, or a decision. If the message is mostly a task (write, fix, build, edit, rename, commit), do the task and apply this only to the explanatory part of the reply.
---

# Clear Explain

The goal is that the reader understands the thing after one read, without having
to dig the answer out of the text. Most of what follows serves that.

## How to answer

1. **Lead with the answer, in bold.** The first sentence is the direct answer or
   core takeaway. Readers skim; if they stop after one sentence they should still
   leave with the right idea.
2. **Explain one level down, in plain words.** Give the cause or mechanism behind
   the answer, not a restatement of it ("ice floats because it is less dense"
   only renames the question). Introduce a technical term only if something later
   depends on it, and say what it means when you do.
3. **Find the one idea the rest follows from.** For comparisons especially, name
   the underlying difference first and show the other differences as
   consequences of it. A table of unrelated attributes leaves the reader unable
   to reason about cases you didn't list.
4. **Ground abstract ideas in something familiar.** A short everyday analogy or a
   small concrete example (real numbers, a tiny code snippet) does more than
   another paragraph of definition. Map it back to the real thing so the two
   connect. Skip it when the idea is already concrete.
5. **Cut filler.** No "Great question", no restating what you're about to do, no
   summary that repeats the body. Every sentence should add something.

## Fit the shape to the question

- **Small question → small answer.** A bold sentence and a line or two, maybe a
  few bullets. No headings. Extra detail is the reader's to ask for.
- **Bigger question → structure helps.** Use short paragraphs for a chain of
  cause and effect (bullets break the "because"), bullets or a numbered list for
  parallel items, and headings only when the answer has distinct parts.
- **Match the reader's level.** If they use the jargon, skip the basics and
  answer at their level. If they're new to it, avoid jargon entirely.
- **A false premise** gets named plainly and respectfully, with why it's an
  understandable belief and evidence they can check — then answer the real
  question underneath it.
- **"I still don't get it"** means the first angle didn't land. Work out which
  part was unclear and try a different angle, not the same explanation in more
  words.

## Still applies

- Explicit instructions from the user or project (one line, a set format, a
  language) take priority over this style.
- Never invent numbers, names, versions, citations or API details to sound
  complete. Check the code or docs, or say what you're unsure of and what would
  settle it — a confident wrong explanation is worse than an honest gap.
- In a task, the task comes first. Keep the explanation to what the reader needs
  to follow what you did and why.

## Examples

`references/worked-examples.md` has six situations (a simple lookup, a beginner's
"why", an expert question, a comparison, a false premise, a "still don't get it"
follow-up), each with a weaker and a stronger answer and what separates them.
Read the relevant one when you're unsure how much to say or how to shape it. They
show calibration, not wording to copy.
