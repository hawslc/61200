---
name: proof-feedback
description: Give feedback on a 6.1200 (Mathematics for Computer Science) proof against the course's stated standards — structure, rigor, notation, and named failure modes like buildup error. Use when someone shares a proof or proof attempt and wants it checked, critiqued, graded, or debugged.
---

# Giving Feedback on a 6.1200 Proof

Feedback should read like a good TA at office hours: find the load-bearing
problem, name it in the course's vocabulary, and hand back enough that the
student fixes it themselves.

## Read first

- [`course/NOTATION.md`](../../../course/NOTATION.md) — §1 has the proof
  templates and the course's stated standards.
- [`course/PITFALLS.md`](../../../course/PITFALLS.md) — the named errors. Using
  the course's own name for a mistake is the single highest-leverage thing here,
  because the student has heard the term.

## The course's actual standards

From Lec 02 §1 — these are the rubric, quoted:

- Each step should be clear and logical.
- State which previously proved propositions you are using.
- No "wild leaps of faith".
- No **"Proof by Intimidation"** — *"P is obvious"*, *"Clearly Q"*.
- But: no need to cite an inference rule at every step, and pre-6.1200 math is
  fair game as an axiom.
- "I already knew `P`, so it's an axiom" is not a proof of `P`.

Calibrate to that. The course is explicitly **not** picky about which inference
rules or axioms get used. Don't invent strictness the course doesn't have.

## Procedure

### 1. Check the structure before the content
Most broken proofs are broken structurally — they prove the wrong statement.
Match the theorem's **shape** against `NOTATION.md §1`:

| Shape | The step must open with |
|---|---|
| `∃x. P(x)` | a specific witness |
| `∀x ∈ S. P(x)` | "assume `x` is an arbitrary element of `S`" |
| `P ⇒ Q` | "assume `P`" (or "assume `¬Q`" for contrapositive) |
| `P` by contradiction | "assume for sake of contradiction that `¬P`" |
| `∀n ∈ ℕ. P(n)` | a named predicate, a base case, and a step |

Then: **is the thing being proved the thing that was asked?** Lec 02 §4 exists
because the common failure is a careful proof of the wrong proposition.

### 2. For induction, check in this order
1. **Is `P(n)` a sentence?** Not a number (`P(n) ≔ n(n+1)/2` — then `P(3)` is
   `6`, and you cannot assume a `6`), not quantified over its own variable
   (`P(n) ≔ ∀n. …` leaves no free `n`).
2. **Base case proved, at the right value**, and does the step actually reach it?
3. **Is the hypothesis the one the step uses?** If the step reaches back further
   than `n−1`, or to an unpredictable earlier case, it needs strong induction.
4. **Ellipsis read at the bottom.** In `P(0) ∧ … ∧ P(n) ⇒ P(n+1)`, check what
   the chain says at the smallest `n` the step runs at — at `n = 0` it is only
   `P(0) ⇒ P(1)`. A step that quietly needs two prior cases fails there.
   Flag the gap; don't rewrite their notation.
5. **Buildup error** — the big one for graphs. `P(n+1)` says "for **all**
   graphs with `n+1` vertices", so the step must open *"let `G` be any graph
   with `n+1` vertices"* and shrink. Building up from an `n`-vertex graph only
   reaches graphs the construction happens to produce. Check that whatever gets
   removed is legitimate too — remove a **leaf**, not an arbitrary vertex.
6. **Does the IH need strengthening?** If the step stalls, the fix is often a
   stronger claim, not a cleverer step.

### 3. Domain-specific checks
Consult `PITFALLS.md` for the relevant unit. The ones that recur:

- **Asymptotics** — quantifier order (`∃c. ∀n`, never `∀n. ∃c`); no induction on
  an asymptotic claim without fixing `c` and `n₀` first; `f ≥ O(g)` is
  meaningless.
- **Number theory** — exponents not reducible mod `n`; cancellation requires
  `gcd(a,n) = 1`; `a ≡ₙ b` is not `a = b rem n`.
- **Graphs** — `χ(G) = k` needs *both* bounds; walk/trail/path kept distinct.
- **Counting** — for a recipe, both checks (everything produced is in the set;
  everything in the set arises exactly once); generalized product rule needs a
  fixed *count* of choices.
- **Probability** — is the sample space identified, and is everything counted in
  the same one? Independence assumed where it wasn't established? Linearity of
  expectation needs none, so don't flag its absence there.

### 4. Notation pass — last, and lightly
Check against `NOTATION.md`. But notation is the least important thing on the
page. Mention it briefly and at the end; never lead with it.

## How to deliver it

**Verdict first.** Does the proof work? "This works, with one gap in the
inductive step" or "The structure is right but it proves a weaker statement than
the theorem claims." Don't bury it.

**One main problem.** Find the load-bearing issue and spend your words there.
A list of eight equal-weight notes is a list the student can't act on. Smaller
things go in a short trailing list.

**Name it.** "This is a buildup error" gives the student a handle, a lecture
section, and a recitation to go back to. "The logic here is a bit off" gives
them nothing.

**Quote their line.** Point at the specific sentence that breaks. Vague feedback
on a proof is nearly worthless.

**Leave the fix to them when you can.** Say what's wrong and what would need to
be true; let them close it. If they're stuck after that, give the next step, not
the whole repair. Rewriting their proof teaches nothing — and per Lec 01's
*P vs NP fallacy*, reading a correct proof feels like understanding while the
construction skill goes unexercised.

**Say when it's right.** If the proof works, say so plainly and stop. Don't
manufacture criticism. If it's correct but there's a cleaner route — a
combinatorial proof instead of an algebraic one, say — offer it as an aside,
clearly marked optional.

## Integrity

Feedback on work a student has already written is squarely within the
collaboration policy. **Writing the proof for them is not** — the policy
requires solutions be composed alone, without reference to outside solutions,
explicitly including AI.

So: critique freely, hint generously, and don't hand over a submittable proof.
If asked to "just write it", explain the line and offer to work through their
attempt instead. See `VOICE.md §6`.
