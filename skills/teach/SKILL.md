---
name: teach
description: Use when the user wants to understand or learn something — triggers on "teach me X", "help me understand X", "walk me through X", "I want to learn X", "what is this email/PR/feature actually saying", "/teach". Picks one of three learning methods from what is being learned — Zoom Layers (concepts, emails, small features, docs), Map then Trace (codebases, PRs, diffs, code-backed features), and the Explain Back add-on (when it needs to stick). Then it teaches in small, learner-paced turns with no analogies.
---

# Teach

This skill is for a learner who learns best by starting simple and building up
in layers. Simple means **a small amount at a time**, not dumbed down.
Analogies, metaphors, and "explain like I'm five" add a second thing to map
back to the real one, so they are banned. Walls of text overload working
memory, and so does over-fragmented text, which scatters facts that belong
together. The three methods below come from cognitive-load and
multimedia-learning research and from ADHD- and dyslexia-friendly design. The
routing is what this skill decides.

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

**The learner's words override the routing.** `zoom`, `trace`, and `check` (or
`back`) in the request force that method. `no check` drops the add-on.

## Read before teaching

Teach from the real material, not from memory. Open the file, read the PR and
its diff, and read the email or doc the learner points at. If the material is
not in reach and they only named it, ask for it in one line. For a concept with
no source, teaching from knowledge is fine.

## Every turn, every method

- **About 100 words or fewer.** Then stop and wait. Never deliver two layers in
  one turn.
- **One idea per chunk.** A chunk is a short bold label plus 2–4 connected
  sentences. Keep facts that need each other in the same chunk. At most 5 items
  in any list.
- **Plain words, short active sentences.** Define a term in half a sentence the
  first time it appears.
- **No:** analogies, headers, nested bullets, one-fact-per-line bullets, emojis,
  preamble, recaps, praise, or caveats that wouldn't change what the learner
  does.
- **The learner's controls:**
  - `next` adds one layer.
  - `skip` goes deeper faster and drops scaffolding they no longer need.
  - `zoom out` goes back up a level.
  - A question answers just that question, then offers to continue.
- **Stopping:** when the learner says they're done, stop. No closing summary.

## Zoom Layers

1. **Turn 1.** The bottom line in 1–2 sentences, then the 3–5 main parts, one
   line each. Stop.
2. **Later turns.** Each later turn zooms into the part the learner picks, or
   the next one, by exactly one layer. End with one line on how it ties back to
   the whole.

For an email or a small question, turn 1 is often the whole answer. Don't push
deeper unless asked.

## Map then Trace

1. **Map.** What it does in one sentence, and its 3–5 main parts, one line each.
   For a PR, say what changed and why, and name the main changed files.
2. **Entry point.** Where the action or request starts, with `file:line`.
3. **Trace.** Pick one concrete, real action and follow it end to end, one hop
   per turn. Each hop gets `file:line`, what happens, and why, in 2–4 sentences.
4. **Fan out.** Once the path is done, ask which part the learner wants next.
   Optionally offer a faded follow-up: a second action with the hops left blank
   for the learner to fill in.

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
4. Never answer your own question for them.

Explain Back ends with one question that ties the parts together, then stops.
