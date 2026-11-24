# teach

`teach` is a Claude Code skill that teaches you one small layer at a time. It
reads what you want to learn, picks one of three learning methods, and then
explains in short turns that wait for you before going further.

It was built for learners who do best with small amounts of information at a
time. That includes many people with ADHD or dyslexia. Walls of text don't work
for them, and neither do answers chopped into dozens of one-line bullets. The
skill bans analogies and "explain like I'm five" framing. "Simple" here means
less at once, not dumbed down.

## Install

Add this repository as a plugin marketplace, then install the plugin:

```bash
claude plugin marketplace add danielfullerton/teach
```

```bash
claude plugin install teach@teach
```

Start a new Claude Code session after installing. Sessions that are already
open don't load new skills.

## Use

Ask in plain words, or call the skill directly:

```text
/teach how OAuth refresh tokens work
teach me what this PR changes: https://github.com/OWNER/REPO/pull/123
help me understand what this email is asking me to do
/teach trace src/server.ts
```

The first turn names the method it picked, for example
`Map then Trace — this is a codebase.`. If the pick is wrong, say so and it
switches.

## The three methods

| Method | Used for | Shape |
| --- | --- | --- |
| Zoom Layers | Concepts, emails, messages, docs, and features described in words. This is the default. | The bottom line in 1–2 sentences and the 3–5 main parts. Each later turn zooms into one part by one layer. |
| Map then Trace | Codebases, folders, PRs, diffs, stack traces, and flows such as runbooks. | A map of the main parts, then the entry point, then one real action traced end to end, one hop per turn with `file:line`. |
| Explain Back | An add-on to either method, for material you need to keep. | After each layer, one short open question. Your answer gets a correction of the single biggest gap. |

### How the skill picks

- **Map then Trace:** used when the subject has code underneath it.
- **Zoom Layers:** used for everything else, and whenever the choice is unclear.
- **Explain Back:** added when your request says "learn", "study", "remember",
  "master", "quiz me", or "make it stick". It's also added for something you'll
  own or maintain. It stays off for one-off reading, such as an email.

To force a choice, put one of these words in your request:

- `zoom` forces Zoom Layers.
- `trace` forces Map then Trace.
- `check` or `back` adds Explain Back.
- `no check` removes Explain Back.

### Controls during a lesson

- `next`: add one layer.
- `skip`: go deeper faster and drop the beginner scaffolding.
- `zoom out`: go back up a level.
- Any question: get an answer to just that question, then an offer to continue.

## Format rules

Every turn, in every method, follows these rules:

- About 100 words or fewer, then a stop.
- One idea per chunk: a short bold label plus 2–4 connected sentences.
- No more than 5 items in any list.
- Plain words and short active sentences, with each term defined the first time
  it appears.
- No analogies, headers, nested bullets, emojis, preamble, recaps, or praise.

## Use the methods in other AI tools

Tools without Claude Code skills, such as ChatGPT or Microsoft Copilot, can run
the same methods from a pasted prompt.

**Zoom Layers**

```text
Use Zoom Layers to help me understand <X>. Start with the bottom line in 1–2 sentences, then the 3–5 main parts, one line each. Stop. When I pick a part or say "next", add one layer: under 100 words, short connected paragraphs, plus one line on how it ties back to the whole. No analogies, no headers, no filler. If I say "skip", go deeper faster.
```

**Map then Trace**

```text
Use Map then Trace on <repo/PR/doc>. Turn 1: what it does in one sentence and its 3–5 main parts, one line each. Turn 2: the entry point (for a PR, the main changed file). Then trace one real input end to end, one hop per turn, with file:line. Stop after each hop. When the path is done, ask which part I want next.
```

**Explain Back** (add it to either prompt above)

```text
Add Explain Back: after each layer, ask me one short open question about just that layer and wait. When I answer, tell me what's right and the single most important gap, in 2–3 sentences. No praise.
```

## Research behind the methods

The methods combine findings from learning science, instructional design, and
studies of AI tutors:

- **Segmenting.** Learner-paced chunks improve retention and transfer. This
  comes from Mayer's segmenting principle, backed by a 2018 meta-analysis of 56
  studies ([Rey et al.](https://doi.org/10.1007/s10648-018-9456-4)).
- **Pretraining.** Learning the key parts before how they interact reduces
  load. This is Mayer's pretraining principle.
- **Elaboration Theory.** Reigeluth's model starts from a core idea, zooms into
  one part, and zooms back out. Zoom Layers follows it, as does BLUF ("bottom
  line up front").
- **Retrieval practice and self-explanation.** These rank among the most
  effective study techniques
  ([Dunlosky et al., 2013](https://pubmed.ncbi.nlm.nih.gov/26173288/)).
  Retrieval helps students with ADHD about as much as their peers
  ([Minear et al., 2023](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2023.1186566/full)).
  Failed recall gave no benefit in an earlier ADHD study (Dudukovic et al.,
  2015), so Explain Back keeps its questions small and asks them right after
  each chunk.
- **Working memory and reading.** In ADHD, reading comprehension drops as
  working-memory load rises
  ([Kofler et al., 2018](https://psy.fsu.edu/clc/Publications/Kofler%20Spiegel%20et%20al.%20(2018)%20Working%20memory%20reading.pdf)).
- **Split attention.** Information that has to be understood together is
  harder to learn when it's scattered. That is why the format rule is "one idea
  per chunk", not one fact per bullet.
- **Expertise reversal.** Scaffolding that helps beginners slows down people who
  already know the material. That is why `skip` exists.
- **Step-by-step AI tutoring.** A Harvard randomized trial found an AI tutor
  that replied in a few sentences, one step at a time, beat an active-learning
  class ([Kestin et al., 2025](https://pmc.ncbi.nlm.nih.gov/articles/PMC12179260/)).
  An AI that hands out answers lowered later exam scores
  ([Bastani et al., 2025](https://knowledge.wharton.upenn.edu/article/without-guardrails-generative-ai-can-harm-education/)).
- **Code reading.** Experienced developers read code in the order it runs.
  Map then Trace follows the same order
  ([Ko and Myers, 2003](https://www.cs.kent.edu/~jmaletic/cs69995-PC/papers/Ko'03.pdf)).

The skill doesn't use the Feynman technique. Its "explain it simply" step tends
to produce analogies and oversimplification, and no studies test the technique
directly.

## License

[MIT](LICENSE)
