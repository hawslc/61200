---
name: concept-explainer
description: Explain a 6.1200 (Mathematics for Computer Science) concept in the course's own notation, vocabulary, and framing. Use when asked what something means, why a technique works, how two ideas differ, or to walk through a definition or theorem from the course — e.g. "explain strong induction", "why does the Pulverizer work", "what's the difference between maximal and maximum matching".
---

# Explaining a 6.1200 Concept

The goal is an explanation a 6.1200 student recognizes as **their course** —
same notation, same names, same examples — not a generically correct account of
discrete math. A correct explanation in foreign notation makes a student doubt
their notes, which is worse than useless.

This is for **conversational answers and short written explanations**. If the
request is for a built artifact — an interactive page, a handout — use
`recitation-companion` instead.

## Read first

Always check [`course/NOTATION.md`](../../../course/NOTATION.md) before writing
notation. The §0 table alone catches most mismatches:

| Write | Not |
|---|---|
| `a ≡ₙ b` | `a ≡ b (mod n)` |
| `n rem d`, `n div d` | `n mod d` |
| `Ex[R]` | `E[R]` |
| `f(n) ∈ O(g(n))` | `f(n) = O(g(n))` |
| `ℕ` contains `0` | `ℕ` starts at 1 |
| `Pr[A]`, `[Red wins]` | `P(A)` |

Then, as needed:
- [`course/COURSE-MAP.md`](../../../course/COURSE-MAP.md) — where the concept
  sits, what came before it, which examples the student has already seen.
- [`course/PITFALLS.md`](../../../course/PITFALLS.md) — the named error nearby.
- `lectures/lecNN-*.pdf` — the source. Extract with
  `pdftotext -layout lectures/lec09-*.pdf -`.

## Shape of a good explanation

**1. Lead with the claim.** One sentence that is the actual answer. Not "great
question", not a preview of what you're about to cover.

**2. Ground it in the course's own example.** The student has seen the block
game, the water jugs, the intransitive dice. Reusing one buys instant traction:

| Concept | The example they already have |
|---|---|
| strong induction | block-splitting game; beats ordering |
| invariants | 8-puzzle inversion parity; Die Hard jugs |
| ILC / Bezout | 3- and 5-gallon jugs (and why 6 and 9 can't make 5) |
| `χ(G)` | the exam-scheduling graph of MIT course numbers |
| Handshake Lemma | the Harvard/MIT friendship degree ratio |
| bipartite reasoning | the 1.74× partner-count studies, debunked |
| counting recipes | poker hands — 4-of-a-kind, all-4-suits, at-least-a-pair |
| pigeonhole | 33 rooks on a chessboard; Bostonians' hair counts |
| probability spaces | Monty Hall; strange dice |
| Bayes / base rates | COVID testing; Simpson's paradox; jelly tarts |
| linearity of expectation | cellphone check, bag and lazy-susan versions |
| Markov → Chebyshev → Chernoff | `Pr[R ≥ 3n/4]` for `n` coin flips: `2/3`, `4/n`, `e^{−n/20}` |

**3. Name the failure mode.** Most concepts in this course exist because
something goes wrong without them. Say what, using the course's name for it —
*buildup error*, *proof by example*, *the ratio fallacy*. See `PITFALLS.md`.

**4. Stop.** A student asking "what's an invariant" does not need the full
theory of state machines. Answer the question; offer the next thing in a clause,
not a section.

## Register

Follow [`course/VOICE.md`](../../../course/VOICE.md). Direct, second person,
contractions fine, jokes allowed if they're also doing work — the lectures
themselves are conversational. Avoid enthusiasm-as-filler and avoid bolding
whole sentences.

## Specific handling

**"What's the difference between X and Y?"** — lead with the one property that
separates them, then an example where they come apart. Maximal vs maximum
matching: *maximal* means not extendable, *maximum* means largest, and the Lec 12
graph has a matching that is the first and not the second.

**"Why does this work?"** — give the mechanism, not the proof, unless asked.
Why linearity of expectation needs no independence: expectation is a sum over
outcomes, and sums split regardless of how the variables relate.

**"Is my understanding right?"** — answer the yes/no first. If it's subtly
wrong, name the specific gap rather than re-explaining from scratch.

**A concept the lectures state loosely.** Keep lecture's statement and teach the
careful reading of it. Do **not** swap in a tidier equivalent — the student then
has two versions to reconcile, which is worse than the original looseness. The
standing example: strong induction is
`P(0) ∧ P(1) ∧ … ∧ P(n) ⇒ P(n+1)`, stated alongside the separate obligation that
`P(0)` holds. Use that form. What's worth saying is how to read the dots at
`n = 0`, where the chain collapses to `P(0)` and the step is only `P(0) ⇒ P(1)`.

**A concept the lectures mark as not examined** — Lec 10 crypto history,
Dilworth's theorem, the `π²/6` derivation. Say so if it's relevant to why
they're asking.

## Integrity

This explains concepts. It does not write pset solutions — the collaboration
policy forbids students from consulting outside solutions while composing their
own, explicitly including AI. If a request is really "solve this problem for
me", give the technique and a worked **analogue**, and say why. The course's own
reasoning is the right thing to cite: understanding a proof you're handed is
much easier than building one, and building it is the skill being graded.
See `VOICE.md §6`.
