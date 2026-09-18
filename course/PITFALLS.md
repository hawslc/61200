# Named Pitfalls

Mistakes 6.1200 calls out **by name** in lecture, plus the ones the notes spend
real time on without naming. Using the course's own vocabulary for an error is
the fastest way to make feedback land — the student has heard the term.

Ordered by where they first appear.

---

## Proof technique

**Proof by Example** (Lec 01)
Checking finitely many cases is not a proof. Anchor: `n² + n + 41` is prime for
`n = 0, …, 39` and composite at `n = 41`. Also Euler's `a⁴ + b⁴ + c⁴ = d⁴`
conjecture, disproved after 200 years by a counterexample with six-digit terms,
and `313(x³ + y³) = z³`, whose smallest counterexample has over 1000 digits.

**Proof by Intimidation** (Lec 02)
"P is obvious." "Clearly Q." Named and banned outright in the course's stated
proof standards.

**Confusing an implication with its converse or inverse** (Lec 01)
`A ⇒ B` is equivalent to its contrapositive `¬B ⇒ ¬A`, **not** to its converse
`B ⇒ A` nor its inverse `¬A ⇒ ¬B`. The lecture's examples: `<3` vs `<4` as
affection intensifiers (`x < 3` is the *stronger* claim), and "I think therefore
I am" vs the meme "I do not think therefore I do not am" (the inverse).

**The P vs NP fallacy** (Lec 01, collaboration policy)
Believing that because you followed someone's proof, you could have produced it.
Verification is easier than construction. This is the stated reason for the
write-up-alone rule, and a good thing to name when a student says "I understood
it when I saw it".

---

## Induction

**Predicate isn't a sentence** (Rec 03 companion §1)
Two failure shapes:
- `P(n) ≔ n(n+1)/2` — a *number*. `P(3)` is `6`, and you cannot assume a `6`.
- `P(n) ≔ ∀n. …` — no free `n` left to vary, so `P(3)` and `P(4)` say the same
  thing and the induction cannot move.

**Misreading the ellipsis at small `n`** (Rec 03 companion §2)
In `P(0) ∧ P(1) ∧ … ∧ P(n) ⇒ P(n+1)`, the dots are suggestive, not literal. At
`n = 0` the chain collapses to the single term `P(0)`, so the step is only
`P(0) ⇒ P(1)` — `P(1)` is not available to assume. Whenever the chain is
written, check what it says at the smallest `n` the step runs at.

**Expecting the base case to come out of the strong step**
Lecture states strong induction as **two** conditions: `P(0)` is true, *and* the
step holds for all `n`. The base case is a separate obligation you owe
independently, just as in ordinary induction.

**Too weak an induction hypothesis** (Lec 02 §5.3)
The thing you prove is also the thing you assume, so a weak claim gives a weak
assumption. Canonical: `2ⁿ × 2ⁿ` L-tromino tiling needs the stronger "cover any
`2²ⁿ − 1` squares" claim; the halving sum needs `= 1 − 1/2ⁿ`, not `< 1`.
Course line: *"if at first you don't succeed, try something harder."*

**Buildup error** ⚠ (Lec 11 §2.5, Rec 11, revisited Lec 13)
The signature graph-induction mistake. `P(n+1)` says "for **all** graphs with
`n+1` vertices", so the step must begin *"suppose `G` is any graph with `n+1`
vertices"* and then **shrink** it. Starting from an arbitrary `n`-vertex graph
and adding a vertex only reaches graphs your construction happens to build.
Lec 13 models the fix when pruning a leaf: *"It's tempting to say 'let `T` be a
tree with `n` vertices', but that's not what `P(n+1)` asks for."*

Related: when you do shrink, shrink correctly. Remove a **leaf**, not an
arbitrary vertex — removing an internal vertex disconnects the tree, and what
remains isn't a tree at all.

**Induction and asymptotics don't mix** (Lec 06 §5)
The `False Claim` that `2ⁿ = O(1)`, with a `Bogus Proof` by induction. Each
statement proved (`2¹ ∈ O(1)`, `2² ∈ O(1)`, …) is *true* — they're about
constant functions — but none of them is the claim. The real error is
**quantifier order**: induction gives `∀n. ∃c`, big-O requires `∃c. ∀n`. To
induct on an asymptotic bound, **fix `c` and `n₀` first** and prove the concrete
inequality.

---

## Asymptotics

**Big-O as a lower bound**
`f ≥ O(g)` is meaningless. The lecture's line: *like saying "you must be at
least 60 inches or less to ride this roller coaster."* Use `Ω`.

**Reading `=` in `f(n) = O(g(n))` as equality**
It is set membership. The course prefers `∈`, tolerates `≤`, and calls `=` "ew,
but most common".

**Trusting the limit test unconditionally**
`lim f/g` existing and finite proves `f ∈ O(g)`; `= ∞` disproves it. But a
**nonexistent** limit settles nothing — fall back to the definition.
`3 + sin(n) ∈ O(1)` despite the limit not existing.

**`∼` absorbs constant factors** — it doesn't.
`n² − n ∼ n²` (quotient → 1), but `n² ≁ n²/2`. Asymptotic equivalence drops
lower-order terms only. Relatedly, `Hₙ ∼ ln n + γ` is vacuous, since `γ` is a
lower-order term; the meaningful statement is `Hₙ − ln n ∼ γ`.

---

## Number theory

**`mod` used two ways** (Lec 09 §3.2)
`a ≡ b (mod n)` is a *relation*; `a mod n` meaning `rem(a, n)` is a *function*.
So `a = b mod n` is ambiguous. The course's fix: write **`a ≡ₙ b`** and
**`a rem n`**, never `mod` as an operator.

**Assuming `a ≡ₙ b` means `a = b rem n`**
`12 ≡₅ 17` is true; `12 ≠ (17 rem 5) = 2`. Neither side of a congruence needs to
be reduced.

**Negative remainders**
In this course `a rem n` is always in `[0, n)`. `(−43) rem 10 = 7`. Many
languages disagree — Lec 09 lists them.

**Reducing exponents mod `n`** ⚠
You may substitute congruent values for **bases**, not **exponents**.
`1 ≡₅ 6` but `2¹ ≢₅ 2⁶`. Fermat's Little Theorem is the licensed exception, and
it reduces exponents mod `p − 1`, not mod `p`.

**Cancelling without an inverse**
`3x ≡₆ 3` does not give `x ≡₆ 1` — `3 · 5 ≡₆ 3` too. You may cancel `a` only
when `gcd(a, n) = 1`.

---

## Graphs

**Confusing "connected" with "adjacent"** (Lec 13)
Connected means a walk exists; adjacent means an edge exists. Every vertex is
connected to itself via the length-0 walk.

**Walk / trail / path used interchangeably**
Strict hierarchy: walk (anything), trail (no repeated *edges*), path (no
repeated *vertices*).

**Euler terminology** (Lec 13, flagged by the lecture as a minefield)
"An Euler cycle is not necessarily a cycle; an Eulerian path is not necessarily
a path, nor does it make a graph Eulerian."

**Proving `χ(G) = k` with only one bound** (Lec 11)
You need both: a `k`-coloring (upper) *and* an argument that `k−1` is impossible
(lower). Exhibiting a coloring alone proves `χ(G) ≤ k`.

**maximal ≠ maximum** (Lec 12)
Maximal = not extendable. Maximum = largest. The lecture gives a matching that
is the first and not the second.

**Critical path size vs path length** (Lec 14)
A critical path is a **set of vertices**; its size is a vertex count, one more
than the length of the corresponding path.

**Mixing directed and undirected edges** (Lec 14)
Never done in this course. A bidirectional road is modelled as two directed
edges.

---

## Counting

**Generalized product rule when the *count* of choices varies** (Lec 16)
The set of choices may change; the **number** may not. Negative example:
increasing 3-digit serials — if the first digit is 7 there's one choice for the
second, if it's 0 there are eight.

**A recipe that isn't a bijection** (Lec 16)
Two checks, always: does every recipe produce something in the target set, and
does every element arise from **exactly one** recipe? The all-4-suits count is
2-to-1 (rescued by the division rule). The at-least-one-pair count is not
`k`-to-1 for any `k` — some hands arise 2, 3, 4, or 6 ways — so it must be done
by complement instead.

**Forgetting pigeonhole is nonconstructive** (Lec 17)
It proves two Bostonians have the same hair count; it does not find them.

---

## Probability

**Skipping the probability space** ⚠ (Lec 18 §4)
The cardinal sin of the unit. The worked error counts successes as *unordered*
sets and the total as *ordered* lists, giving nonsense. **Fix the sample space
first**, then let it dictate what you count.

**Skipping Step 0** (Lec 18)
Monty Hall has no answer until you state modelling axioms. Tricksy Monty (offers
a switch only when you picked the car) and benevolent Monty (only when you
didn't) are both consistent with Craig's letter and give opposite answers.

**Assuming intuition transfers**
The "beats" relation need not be transitive — Red beats Green beats Blue beats
Red, each with probability 5/9, and the order *reverses* on two rolls.

**Confusing likelihood with posterior** (Lec 19)
`Pr[A | B] ≠ Pr[B | A]`. The COVID example: a test with a 0.1 false-negative
rate still leaves you more likely healthy than sick after a positive result,
because the base rate dominates.

**Ignoring the prior / base rate** (Lec 19)
Simpson's paradox and the jelly-tart argument are both base-rate failures. In
the jelly-tart case *both* sides are wrong because both condition on the wrong
event — the relevant probability is `Pr[C | J ∩ X]`, not `Pr[C | J]`.

**Pairwise independence assumed to be mutual** (Lec 20)
Three fair coins, `A` = "coins 1,2 agree", `B` = "2,3 agree", `C` = "3,1 agree".
All pairs independent; the triple is not.

**Assuming independence across correlated events** (Lec 20)
The 2016 election: multiplying three state probabilities gives 0.008, but
systematic poll error correlates them. With no correlation assumptions, the best
upper bound is the smallest individual probability.

**Conditioning creates dependence**
Two independent traits become anticorrelated once you condition on "at least one
of them holds". No causal link required.

**Gambler's fallacy** (Lec 20) — and its inversion. After 50 heads the
*rational* update is toward the coin being biased, i.e. predicting heads again —
the opposite of "due for tails".

**Confusing the three expectation formulas** (Lec 22 §6)
`Σ_ω R(ω)Pr[ω]` (over outcomes) vs `Σ_x x·Pr[R=x]` (over values) vs linearity
(over RVs). The lecture warns these get merged into things like `Σ_ω ω·Pr[ω]`.

**The ratio fallacy** (Lec 23 §3)
`Ex[R/T] > 1` does **not** imply `Ex[R] > Ex[T]`, and `Ex[1/R] ≠ 1/Ex[R]`. The
bogus proof assumes `Ex[T] > 0` and that `R/T` and `T` are independent. The
RISC/Z8002 benchmark table is the punchline: averaging `Z/R` "proves" Z8002 is
20% more verbose, averaging `R/Z` "proves" RISC is 10% more verbose. Average the
quantities, not the ratios.

**Requiring independence for linearity of expectation**
Never needed. This is what makes it powerful — the cellphone indicators are very
much not independent, and linearity works anyway.

**Applying Markov to a signed RV** (Lec 24)
Non-negativity is required. Counterexample: `R = ±1` on a fair coin has
`Ex[R] = 0`, yet `Pr[R ≥ 1/2] = 1/2`. Instead **adjust the bound**: if `S ≥ ℓ`,
apply Markov to `S − ℓ`; if `S ≤ u`, apply it to `u − S`.

**Adding standard deviations** (Lec 24)
Variances of pairwise independent RVs add. Standard deviations do not —
`σ(R₁+R₂)² = σ(R₁)² + σ(R₂)²`.
