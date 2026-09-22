# 6.1200 Course Map — Fall 2026

Lecture-by-lecture index: what is covered, what a companion for it would be
about, and which recitation it pairs with. Built from `lectures/` (gitignored).

**Cadence.** Lectures Tu/Th. Recitations W/F, attendance graded (10%), run as
group problem-solving. A **WU** (warm-up, instant feedback, unlimited tries) is
due before every recitation. Problem sets — called **PEST** in the notes — are
released Wednesdays and due Tuesdays at noon; late work earns `100 − n` percent
at `n` hours late, floored at 50%.

**Collaboration policy** (worth knowing when writing anything student-facing):
solve in small groups, list collaborators per problem or write `Collab: None`,
but **write up alone** — no looking at others' solutions, no communal notes
while composing, no ChatGPT. The stated reason is the **"P vs NP fallacy"**:
verifying someone's proof is far easier than constructing your own, so "in your
own words" means *actually* piecing it together yourself.

> This matters for how these tools should behave. Material here is for
> **teaching and review**, not for producing pset answers. See `VOICE.md §6`.

---

## Unit 1 — Proofs (Lec 01–04)

| # | Lecture | Core content | Pairs with |
|---|---|---|---|
| 01 | Predicates, Sets, and Proofs | proposition/predicate, ∀ ∃ ∧ ∨ ¬ ⇒, truth tables, sets, axioms, consistency/completeness, Gödel | Rec 01 |
| 02 | Contradiction and Induction | inference rules, the five basic techniques, **proof outlining**, `√2 ∉ ℚ`, induction axiom, **strengthening the IH** (tromino) | Rec 02 — geometric series by induction |
| 03 | Casework and Strong Induction | proof by cases, Ramsey `R(3,3) ≤ 6`, Four Color history, **strong induction**, block-splitting game, beats ordering | **Rec 03 — strong induction** ✅ companion exists |
| 04 | State machines | 8-puzzle, preserved predicates, **Invariant Principle**, inversions & parity, derived variables/potential functions, termination | Rec 04 |

Teaching notes:
- Lec 01's "proof by example is not a proof" is anchored by `n² + n + 41`
  (prime for `n = 0..39`, composite at 41) and Euler's `a⁴+b⁴+c⁴=d⁴` conjecture.
  Both are good hooks.
- The Lec 01 "waiter" bit (chicken *or* pasta / coffee *or* tea / cream *or*
  sugar — three English "or"s, none of them `∨`) is the course's way in to why
  formal connectives are worth the trouble.
- Lec 02's outlining example uses nonsense predicates (*fooish*, *barsome*)
  precisely to show the structure comes from the **shape**, not the content.
  That device is reusable.

---

## Unit 2 — Sums, asymptotics, recurrences (Lec 05–07)

| # | Lecture | Core content | Pairs with |
|---|---|---|---|
| 05 | Sums | annuities, geometric series, **perturbation**, **ansatz**, double sums & exchanging order, **Integral Method** (3 theorems) | Rec 05 — incl. `Σ i·xⁱ = x/(1−x)²` (Problem 3) |
| 06 | Asymptotics | block-stacking & `Hₙ`, Stirling, `∼`, `O Ω Θ o ω`, **"Induction and Asymptotics Don't Mix"**, abuses of notation | Rec 06 |
| 07 | Recurrences | Towers of Hanoi, Merge Sort, **Plug and Chug**, **Master Theorem** and its gaps | Rec 07 |

Teaching notes:
- Lec 06's overhang result is a great cold open: to get 10 block-lengths of
  overhang you need `≈ e²⁰ ≈ 400` billion blocks — about 40× the distance to
  the Moon.
- The `2ⁿ = O(1)` bogus proof is the single best quantifier-order lesson in the
  course. A companion on it practically writes itself.

---

## Unit 3 — Number theory (Lec 08–10)

| # | Lecture | Core content | Pairs with |
|---|---|---|---|
| 08 | Divisibility | `a \| b`, **ILC**, Die Hard water jugs as a state machine, gcd, Euclid, **the Pulverizer**, Bezout | Rec 08 |
| 09 | Modular Arithmetic | `a ≡ₙ b`, `rem`/`div` pitfalls, arithmetic mod `n`, inverses, **Fermat's Little Theorem**, divisibility-by-9, ISBN | Rec 09 |
| 10 | Cryptography | Caesar/substitution/Enigma/one-time pad (**not examined**), Diffie-Hellman, **RSA**, primality & density of primes | Rec 10 — **CRT**, and removing RSA's coprimality assumption |

Teaching notes:
- Die Hard 3's jug puzzle is the motivating example for ILCs; "Die Hard 9" with
  6- and 9-gallon jugs is the impossibility case.
- Lec 09 §3 is a whole section on *confusing notation*. Any companion here
  should spend real time on `rem` vs `≡ₙ` — it is where students actually get
  lost, and the lecture says so.

---

## Unit 4 — Graph theory (Lec 11–15)

| # | Lecture | Core content | Pairs with |
|---|---|---|---|
| 11 | Graphs and Coloring | simple graphs, Handshake Lemma, bipartite average-degree, `χ(G)`, greedy `d+1` bound, NP-completeness | Rec 11 — **buildup error** |
| 12 | Matching | maximal vs maximum, perfect, weighted, **stable matching**, **Gale-Shapley**, feasible/optimal/pessimal | Rec 12 — optimal/pessimal proofs |
| 13 | Connectivity and Trees | **walk/trail/path**, connected components, Königsberg, Euler tours, trees, leaves, `n−1` edges, 6 equivalent characterizations | Rec 13 |
| 14 | Digraphs and DAGs | directed analogs, SCCs, condensation, DAGs, topological order, chains/antichains, parallel scheduling, Dilworth (**not examined**) | Rec 14 — an Euler tour application |
| 15 | Relations and Counting | relations, total/injective/surjective/bijection as arrow counts, equivalence relations, WPOs, product/bijection/sum rules | Rec 15 |

Teaching notes:
- The bipartite degree-ratio argument debunking the "men have 1.74× more
  partners" studies is the unit's showpiece — a real, published error killed by
  the Handshake Lemma.
- Lec 11's exam-scheduling graph is literally built from MIT course numbers,
  with 6.1200 repeatedly stuck with the 1am slot. Keep the joke.
- **Buildup error** gets its own recitation. Treat it as a headline concept.

---

## Unit 5 — Counting (Lec 16–17)

| # | Lecture | Core content | Pairs with |
|---|---|---|---|
| 16 | Counting | generalized product rule, **division rule**, `n choose r`, **counting by recipe**, poker hands | Rec 16 — **bookkeeper rule** |
| 17 | More Counting | **PIE**, **Pigeonhole** + generalized, combinatorial proofs / double counting, Binomial & Multinomial Theorems, Pascal | Rec 17 |

Teaching notes:
- The poker-hand sequence is pedagogically deliberate: a recipe that works
  (4-of-a-kind), one that double-counts but is rescued by the division rule
  (all-4-suits), and one that fails outright because the map isn't `k`-to-1
  (at-least-one-pair, which must be counted by complement instead). That
  *arc* is the lesson, not any single count.
- The 33-rooks-on-a-chessboard diagonal-labelling argument is the best
  "choose your pigeonholes cleverly" example available.

---

## Unit 6 — Probability (Lec 18–24)

Quiz 2 lands just before this unit.

| # | Lecture | Core content | Pairs with |
|---|---|---|---|
| 18 | Introduction to Probability | **Monty Hall**, the **Four Step / Tree Method**, sample spaces, events, uniform spaces, **intransitive dice** | Rec 18 |
| 19 | Conditional Probability | probability rules, `Pr[A\|B]`, product rule, **Bayes' rule**, COVID base rates, **Simpson's paradox**, jelly tarts / O.J. | Rec 19 — birthday problem |
| 20 | Independence | independence, **pairwise vs mutual**, 2016 election correlations, conditional independence, **Birthday Principle**, gambler's fallacy | Rec 20 |
| 21 | Random Variables | RVs as total functions, indicators, PMF/CDF, two-envelope problem, **binomial distribution** | Rec 21 |
| 22 | Expectation | `Ex[R]`, indicator trick, mean time to failure, **linearity of expectation**, cellphone check | Rec 22 |
| 23 | Expectation (cont.) | counting events, **union bound** via expectation, `Ex[R₁R₂]`, **the ratio fallacy** (RISC/Z8002) | Rec 23 — `Var[R] = Ex[R²] − Ex[R]²` |
| 24 | Large Deviations | **Markov**, adjusting bounds, **Chebyshev**, **Chernoff**, concentration | Rec 24 — variance of sums |

Teaching notes:
- Monty Hall is taught as a *modelling* lesson first: the answer depends on
  axioms about Monty's behaviour, and the lecture spells out tricksy-Monty and
  benevolent-Monty as legitimate alternatives. Don't skip Step 0.
- Intransitive dice (Red beats Green beats Blue beats Red, each 5/9 — and the
  order **reverses** when you roll twice) is the unit's best intuition-breaker.
- The cellphone-check problem appears in both the bag version (`Ex[R] = 1`) and
  the lazy-susan version (`Ex[R] = 1`), with wildly different distributions.
  Lec 24 reuses the pair to show Markov is tight for one and off by `n!/n` for
  the other. That's a three-lecture callback — good companion material.

---

## Where companions exist

| For | Topic | File |
|---|---|---|
| Rec 03 | Strong induction: predicates, ordinary vs strong, strengthening | [`companions/rec-03.html`](../companions/rec-03.html) |
| Lec 04 | State machines on tic-tac-toe: states, final states, invariant + reachability, potential function | [`companions/lec-04.html`](../companions/lec-04.html) |

Add a row when you build one.
