# Voice and Pedagogical Standards

How 6.1200 material in this repo should sound and behave. Reverse-engineered
from `companions/rec-03.html` and from the lecture
notes' own teaching habits.

---

## 1. Who you're writing for

A student who has **already been to recitation** and argued the problem at the
board. They are not a beginner and they are not reading this to learn the topic
cold. They came back because something didn't click.

So: no "Welcome to the wonderful world of induction!" No re-teaching from zero.
The opening line of the existing companion is the model —

> *"You've argued these at the board. Here they are stripped down to the parts
> that decide whether a proof actually holds together."*

It assumes competence, names the gap, and promises compression.

---

## 2. Register

**Second person, direct, unhurried.** Contractions are fine. The lecture notes
themselves are conversational — jokes about Pokémon, Downton Abbey, MIT
Confessions, "so on and so fifth" — and material that is stiffer than the
lectures reads wrong.

What to do:
- Short declarative sentences for the load-bearing claims.
- Name the thing that goes wrong, concretely, with the actual wrong expression
  written out.
- Let a sentence be funny if it is *also* doing work.

What to avoid:
- Enthusiasm as filler ("Great question!", "Let's dive in!", "Isn't that
  amazing?").
- Hedging that isn't real ("you might want to perhaps consider").
- Listing what the section will cover before covering it.
- Bold on more than a few words per paragraph. Bold marks the claim, not the
  topic.

**Em dashes and typographic quotes.** The existing companion uses `—` and
`“ ”` / `’` throughout. Match it.

---

## 3. Structure of a companion

Numbered sections, three or four, each a **single idea named as a claim**:

> `1  A predicate is a sentence`
> `2  Ordinary vs. strong induction`
> `3  Sometimes you have to claim more`

Not "Predicates", "Induction types", "Strengthening" — those are topics. The
headings above are assertions, which is what makes the page feel like it is
arguing something.

Each section runs roughly:
1. **Prose** — the claim, plainly, in two or three sentences.
2. **An interactive card** (`Try it`) — the reader manipulates something and
   sees the consequence.
3. **A `note`** — the observation the widget was built to produce. Say it
   outright; don't rely on the reader noticing.
4. Optionally a **check** — a multiple-choice with real distractors.

Close with **"The short version"**: a numbered list where each item is a **bolded
imperative** plus one sentence of why. These are the takeaways a student would
write on an index card.

Footer, exactly this shape:
`6.1200J / 18.062J · a short companion to Recitation NN, Fall 2026.`

---

## 4. Interactivity that earns its place

Every widget in the existing companion answers a question a student actually
asked. None of them are decoration.

| Widget | The confusion it targets |
|---|---|
| Predicate playground — pick `P`, pick `n`, see the sentence | "Is `P(n)` a number or a claim?" |
| Triage — judge whether a candidate can be inducted on | "How do I know if my predicate is well-formed?" |
| Assume-viewer — toggle ordinary/strong, see which slots you get | "What exactly am I allowed to assume?" |
| Halving-sum slider — add terms, watch the gap | "Why doesn't `< 1` work?" |
| Step-through — run the induction under each hypothesis | "Where does the weak version actually break?" |

**The test:** if the widget were replaced by a static sentence, would anything be
lost? If not, write the sentence.

The strongest pattern is the **contrast toggle** — let the reader flip between
the version that works and the version that doesn't, on the same example. That
is what makes "the stronger claim is easier to prove" land instead of sounding
like a paradox.

**Technical constraints** (from the existing file):
- Single self-contained `.html`. No build step, no framework.
- Google Fonts is the only external request. Everything else inline.
- Vanilla JS in an IIFE, `"use strict"`, `var`, feature-guarded
  (`if(!sel) return;`). ES5-flavoured — match it.
- Light/dark via CSS custom properties, with all three selectors:
  `@media (prefers-color-scheme:dark){:root:not([data-theme="light"])}`,
  `:root[data-theme="dark"]`, and the light default on `:root`.
- `aria-pressed` on toggle buttons. Keyboard-reachable controls.
- Max width `760px`, 16px side gutters, works at phone width.

---

## 5. Fidelity rules

**Never invent course content.** If you don't know whether 6.1200 uses a term,
check `NOTATION.md`, then the lecture text. An unfamiliar-but-correct notation
is worse than a familiar one — it makes the student doubt their notes.

**Match lecture's notation, then teach students to read it carefully.** Where a
lecture formulation is loose, the move is *not* to replace it with a cleaner one
— students would then be holding two incompatible statements. Keep lecture's
form and teach the careful reading.

The standing example is strong induction. Lecture writes
`P(0) ∧ P(1) ∧ … ∧ P(n) ⇒ P(n+1)`. The `∀m < n` phrasing is equivalent and
arguably tighter, but swapping it in re-indexes what the step proves and leaves
students reconciling two versions. So `rec-03.html` uses lecture's conjunction
form and spends its ink on the thing that actually trips people up: at `n = 0`
the chain collapses to `P(0)`, so the step is only `P(0) ⇒ P(1)`. Same insight,
no notational fork.

**Reuse the course's own examples.** A student who sees the chocolate bar, the
block-splitting game, or the intransitive dice again gets a free callback. The
recitation-03 companion closes §3 with *"You've seen this before. The
chocolate-bar predicate had to say…"* — that line costs nothing and does a lot.

**Use the course's named pitfalls by name.** *Buildup error*, *Proof by
Intimidation*, *proof by example*, *the P vs NP fallacy*, *gambler's fallacy*,
*the ratio fallacy*. See `PITFALLS.md`.

**Bogus proofs are a course genre.** The lectures present `False Claim.` /
`Bogus Proof.` / *"Where's the error?"* as a deliberate device (Lec 06, Lec 23).
Companions can and should use it — it is native, not a gimmick.

---

## 6. Academic integrity

The collaboration policy (see `COURSE-MAP.md`) forbids students from consulting
outside solutions — explicitly including ChatGPT — while composing their own
proofs.

Material in this repo is for **teaching concepts and reviewing understanding**.
That means:

- **Fine:** explaining a technique, building companions on lecture/recitation
  content, worked examples from lectures, practice problems *with* solutions the
  student reveals after trying, feedback on reasoning a student has already
  written.
- **Not fine:** writing a pset solution for a student to submit, or producing
  something shaped like one.

If a request is ambiguous, prefer the version that makes the student do the
work: a hint, a question back, a worked *analogue* rather than the problem
itself. The course's own stated reason is the right one to give — understanding
a proof someone hands you is much easier than constructing it, and the
construction is the skill being graded.
