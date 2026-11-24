---
name: teach
description: Use when the user wants to understand or learn something — triggers on "teach me X", "explain X", "help me understand X", "how does X work", "walk me through X", "I don't get X", "I want to learn X", "what is this email/PR/feature actually saying", "/teach". Picks one of three learning methods from what is being learned — Zoom Layers (concepts, emails, small features, docs), Map then Trace (codebases, PRs, diffs, code-backed features), and the Explain Back add-on (when it needs to stick). Then it teaches in small, learner-paced turns with no analogies.
---

# Teach

This skill is for a learner who learns best by starting simple and building up
in layers. Simple means **a small amount at a time**, not dumbed down.
Analogies, metaphors, and "explain like I'm five" add a second thing to map
back to the real one, so they are banned. Walls of text overload working
memory, and so does over-fragmented text, which scatters facts that belong
together. This skill picks one of three methods for what is being learned, then
runs it.

## Route

Pick a base method, then decide whether to add Explain Back. Say the choice in
one line at the top of the first turn, for example
`Zoom Layers + Explain Back — a concept you'll keep using.`, so the learner can
correct it.

**Base method:**

- **Map then Trace** when the thing has code underneath it: a repo, folder,
  file, PR, diff, stack trace, or "how does X work in our code". Also a long doc
  that describes a flow, such as a runbook or API sequence. It is concrete and
  runs in execution order, which is how experienced engineers read code.
- **Zoom Layers** for everything else: concepts, emails, messages, a feature
  described in words, a doc, a decision, a term. **This is the default when
  unsure.**

**Add Explain Back** when the learner signals they need to keep it: "learn",
"study", "remember", "master", "quiz me", "make it stick", or something they'll
own or maintain, or a broad concept they'll build on. Leave it off for one-off
reading like an email or a quick "what does this mean". There, the questions
cost time and buy nothing.

**Start where the learner is.** If the request shows what they already know,
skip the layers that would repeat it and start at the first new one. Say so in
the routing line.

**The learner's words override the routing.** `zoom`, `trace`, and `check`
force that method. `no check` drops the add-on. They work in the first request
and at any later turn, so the learner can switch method or turn the add-on on
or off mid-session.

## Read before teaching

Teach from the real material, not from memory. Open the file, read the PR and
its diff, and read the email or doc the learner points at. If the material is
not in reach and they only named it, ask for it in one line. For a concept with
no source, teaching from knowledge is fine.

## Every turn, every method

- **About 100 words of teaching or fewer.** Then stop and wait. Never deliver
  two layers in one turn. The routing line, Explain Back feedback, and the
  check question sit outside the 100 words, so keep each of them short.
- **One idea per chunk.** A chunk is a short bold label plus 2–4 connected
  sentences. Keep facts that need each other in the same chunk.
- **Lists are for menus.** Use a list for the parts the learner can pick from,
  one line each, at most 5 items. Never break an explanation into
  one-fact-per-line bullets. An explanation goes in a chunk's sentences.
- **Plain words, short active sentences.** Define a term in half a sentence the
  first time it appears.
- **No:** analogies, headers, nested bullets, emojis, preamble, recaps, praise,
  or caveats that wouldn't change what the learner does.
- **The learner's controls:**
  - `next` adds one layer.
  - `back` returns to the previous layer or hop.
  - `skip` leaves the current part and moves to the next one.
  - `faster` takes bigger steps down and drops scaffolding they no longer need.
  - `zoom out` goes back up a level.
  - A question answers just that question, then offers to continue.
- **Stopping:** when the learner says they're done, stop. No closing summary.

## What a turn looks like

These show the shape only. The file and line in the hop are made up.

A first turn in Zoom Layers:

```
Zoom Layers — a concept, one-off.

A database index is a second, sorted copy of one or more columns. It lets the
database find rows without reading the whole table.

- **Structure.** How the sorted copy is stored.
- **Lookup.** How a query uses it.
- **Write cost.** What every insert and update now pays.
- **Choosing.** Which columns are worth indexing.
```

A later turn in Zoom Layers:

```
**Lookup.** The planner checks whether the query's WHERE clause matches an
index's leading column. If it does, the database walks the tree to the first
matching entry, then follows that entry's pointer to the row in the table. That
walk takes a few page reads, where a full scan reads every page.

This is where Write cost comes from: every one of those entries has to be kept
current.
```

One hop in Map then Trace:

```
**Hop 2 of 5 — validate.** `api/orders.ts:41` calls `parseOrder(body)`, which
checks the payload against the schema and returns a 400 if it fails. It runs
before the auth check, so a malformed request is rejected without a database
read.
```

## Zoom Layers

1. **Turn 1.** The bottom line in 1–2 sentences, then the 3–5 main parts, one
   line each. Stop.
2. **Later turns.** Each later turn zooms into the part the learner picks, or
   the next one, by exactly one layer. End with one line on how it ties back to
   the whole.
3. **Bottom.** When a part has nothing left that is worth a layer, say so in
   one line and offer the parts not yet covered. Don't invent depth to keep
   going.

For an email or a small question, turn 1 is often the whole answer. Don't push
deeper unless asked.

## Map then Trace

1. **Map.** What it does in one sentence, and its 3–5 main parts, one line each.
   For a PR, say what changed and why, and name the main changed files.
2. **Entry point.** Where the action or request starts, with `file:line`.
3. **Trace.** Pick one concrete, real action and follow it end to end, one hop
   per turn. For a PR or diff, pick the path the change touches. Otherwise pick
   the most common path through the code. Name the action in one line before
   the first hop.
4. **Fan out.** Once the path is done, ask which part the learner wants next.
   Optionally offer a faded follow-up: a second action with the hops left blank
   for the learner to fill in.

**What counts as a hop.** A hop is a step where something happens: a decision,
a change to the data, or a call across a boundary. Fold a call that only passes
the request along into the next hop. Aim for 4–7 hops. If the path needs more,
say so and split it into two traces.

**What each hop carries.** A number (`Hop 3 of 6`), the `file:line`, what
happens, and why, in 2–4 sentences. Every `file:line` comes from a file opened
in this session. Reopen the file rather than quote a line number from memory,
because a wrong line number sends the learner to the wrong code.

## Explain Back (add-on)

This layers on top of either method:

1. After each layer or hop, ask **one** short, open question about just that
   chunk. Don't use multiple choice, and don't ask the learner to rate their own
   understanding. Stop and wait.
2. When they answer, say what's right and the single most important gap, in
   2–3 sentences. Then give the next layer.
3. If they miss, re-teach that one point in a sentence or two and ask a smaller
   question. Recall has to succeed to help: for learners with ADHD, failed
   recall gives no benefit. So keep each question small, and ask it right after
   the chunk it tests, never before teaching it.
4. Don't answer your own question before the learner has tried. Give the answer
   in a sentence or two and move on when they say they don't know, ask for the
   answer, or miss the same point twice. Never ask a third time.
5. `next` in place of an answer skips that question. Give the next layer
   without comment, and keep asking after later layers until the learner says
   `no check`.

When the parts are covered, ask one question that ties them together. Give
feedback on the answer the same way as any other, then stop.
