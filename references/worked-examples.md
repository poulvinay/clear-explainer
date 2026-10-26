# Worked examples

Six situations, each with a weaker answer, a stronger one, and what separates
them. These show calibration, not wording to copy.

1. [A simple lookup](#1-a-simple-lookup)
2. [A beginner's "why"](#2-a-beginners-why)
3. [An expert's technical question](#3-an-experts-technical-question)
4. [A comparison](#4-a-comparison)
5. [A false premise](#5-a-false-premise)
6. [A "still don't get it" follow-up](#6-a-still-dont-get-it-follow-up)

---

## 1. A simple lookup

**Question:** "What does a 404 mean?"

**Weaker:** A headed overview of HTTP status codes, the five status classes, the
history of 404, and a bulleted list of common causes.

**Stronger:**

> **It means the server was reached but has nothing at that address** - the page was
> moved, deleted, or the URL is mistyped. The site itself is working; that
> particular link is not.

**Why:** The question was small. Two sentences answer it and add the one
distinction that is useful (the server is up, the page is missing). Anything more
is the person's to ask for.

---

## 2. A beginner's "why"

**Question:** "Why does ice float?"

**Weaker:**

> Ice floats because it is less dense than water. Density is mass per unit
> volume, and objects less dense than the fluid they are in will float.

This restates the question. "Less dense" is the thing that needed explaining.

**Stronger:**

> **Ice floats because water takes up more room when it freezes, so a piece of ice
> is lighter than the same volume of liquid water** - about 9% lighter.
>
> That is unusual; most substances shrink when they freeze. Water is different
> because of the shape of its molecules. Each one is slightly bent and attracts
> its neighbours at particular angles. In liquid water the molecules are moving
> too fast to hold those angles, so they tumble past each other and pack fairly
> closely. As water freezes they slow down and lock into a fixed pattern of
> six-sided rings, and that pattern has gaps in it. Same molecules, more empty
> space, so lower density.
>
> You can see the expansion directly: a full bottle of water left in the freezer
> bulges or cracks.
>
> It also matters outside the kitchen. Because ice stays on top, lakes freeze
> from the surface down, and the ice layer insulates the water underneath.

**Why:** Answer first, then the cause one level down, in everyday words. The
everyday example is one the reader can check. "Hydrogen bond" and "hexagonal
lattice" were left out because nothing later depended on them; name them if the
person seems to want the vocabulary.

---

## 3. An expert's technical question

**Question:** "My Postgres query filters on `created_at`, there's a btree index
on it, and EXPLAIN still shows a seq scan. Why?"

**Weaker:** Opens by explaining what an index is and how B-trees work, then
suggests "making sure the index exists".

**Stronger:**

> **The planner picks a seq scan when it estimates that is cheaper, so the question
> is which estimate is leading it there.** The usual causes, roughly in order of
> likelihood:
>
> 1. **The filter is not selective.** If the range matches a large share of the
>    table, reading it sequentially beats many random index lookups. Compare the
>    estimated rows in the plan with the table size.
> 2. **The column is wrapped in an expression.** `WHERE date(created_at) = ...`
>    or a cast on the column cannot use a plain index on `created_at`. Rewrite as
>    a range (`created_at >= ... AND created_at < ...`) or add an expression
>    index.
> 3. **Statistics are stale.** If estimated and actual row counts in
>    `EXPLAIN ANALYZE` are far apart, run `ANALYZE` on the table.
> 4. **The table is small.** For a few pages of data a seq scan is the right
>    plan.
>
> I can't tell which applies without the query and the `EXPLAIN (ANALYZE,
> BUFFERS)` output - if you paste those I can narrow it down.

**Why:** The asker already used "btree" and "seq scan", so the basics are
skipped. The answer gives the governing principle (cost estimation) so the list
is not arbitrary, says how to tell the cases apart, and is explicit that it is
not diagnosing a query it has not seen. A numbered list fits because these are
parallel alternatives.

---

## 4. A comparison

**Question:** "What's the difference between a debit card and a credit card?"

**Weaker:**

> | | Debit | Credit |
> |---|---|---|
> | Source of funds | Bank account | Credit line |
> | Interest | No | Yes |
> | Builds credit | No | Yes |

Accurate, but the rows look unrelated and the reader still cannot choose.

**Stronger:**

> **The difference is whose money is being spent at the moment you pay.** A debit
> card takes your own money straight out of your bank account. A credit card
> spends the card issuer's money, and you pay them back later.
>
> Most of the other differences follow from that:
>
> - **Interest.** Borrowed money can be charged for. Pay the full bill each month
>   and you normally pay none; carry a balance and the rates are high.
> - **Credit history.** Repaying borrowed money on time is what a credit record
>   tracks, so credit card use builds one and debit card use generally does not.
> - **When something goes wrong.** With a disputed charge on a credit card, the
>   money in limbo is the issuer's. On a debit card it is yours, already gone from
>   your account until the dispute is settled.
> - **Overspending.** Debit stops at your balance. Credit stops at a limit that
>   may be well above what you can comfortably repay.
>
> My suggestion: if you reliably pay the bill in full, a credit card is the
> better default for everyday spending. If you think you would carry a balance,
> use debit - the interest will outweigh the benefits. (Protections and fees vary
> by country and by card, so check yours.)

**Why:** One underlying difference, with the rest shown as consequences of it, so
the reader can reason about cases not listed. The recommendation is marked as a
recommendation and comes with the condition that reverses it. The closing caveat
flags the part that varies instead of asserting specifics.

---

## 5. A false premise

**Question:** "Why is it summer when the Earth is closer to the sun?"

**Weaker (goes along with it):** An explanation of how proximity to the sun
increases heating.

**Weaker (corrects and stops):** "Actually, that's a common misconception.
Seasons are caused by axial tilt."

**Stronger:**

> **Distance is not what causes the seasons**, though it is a natural guess - getting
> closer to a heat source is how warmth works in everyday life. Two things show
> it cannot be the cause: the Earth is closest to the sun in early January, the
> middle of northern winter; and the two hemispheres have opposite seasons at the
> same time, while being at the same distance.
>
> The real cause is that the Earth's axis is tilted, by about 23 degrees. For
> part of the year the northern half leans toward the sun. Sunlight then hits it
> more directly, so the same energy lands on a smaller patch of ground, and the
> days are longer, so there are more hours of heating. That is northern summer.
> Six months later the Earth is on the other side of its orbit, the northern half
> leans away, and the situation reverses.
>
> The distance does change, by about 3% over the year, but its effect is small
> next to the tilt.

**Why:** It names the wrong assumption, grants that it is reasonable, gives
evidence the reader can check against what they already know, and then answers
the real question (why are there seasons). It also places the grain of truth -
distance does vary - so the reader's old belief is refined, not just overruled.

---

## 6. A "still don't get it" follow-up

**Context:** Recursion was explained as "a function that calls itself with a
smaller input until it reaches a base case", with a factorial example.
**Follow-up:** "I still don't get how it actually gets an answer."

**Weaker:** The same definition again, in more words, with the same factorial
code and more comments.

**Stronger:**

> **Think of a queue where each person only asks the one ahead.** You are in a queue and want to know your
> position, but you can only see the person ahead of you.
>
> You ask them, "what's your position?" They do not know either, so they ask the
> person ahead of them, and so on. Eventually the question reaches the person at
> the front, who does know: "I'm first."
>
> Now the answers travel back. The second person hears "1" and says "2". The
> third hears "2" and says "3". When it reaches you, you add one to what you were
> told.
>
> Nobody counted the whole queue. Each person did one small thing - ask ahead,
> add one - and one person knew the answer outright. That is all a recursive
> function is: the questions going forward are the calls, the person at the front
> is the base case, and the answers coming back are the return values.
> `factorial(4)` asks `factorial(3)` for its answer and multiplies by 4 on the
> way back, exactly as you added one.

**Why:** The confusion was specific - where the answer comes from - so the new
explanation targets the return path, which the first one glossed over. It uses a
different angle instead of repeating the first, and then maps the analogy back
onto the original example so the two connect.
