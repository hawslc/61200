# 6.1200 Notation and Conventions

The authoritative reference for writing 6.1200 material. Every claim here is
drawn from the Fall 2026 lecture notes (`lectures/`, gitignored). Where the
course differs from common textbook practice, that difference is **marked
`⚠ COURSE-SPECIFIC`** — those are the ones that make material read as authentic
or as foreign.

Course: **6.1200J / 18.062J, Mathematics for Computer Science**, MIT, Fall 2026.
Staff: Z. Abel, T. Leighton, R. Williams.

---

## 0. The high-value differences

If you remember nothing else, remember these six. Each is a place where the
default habit produces something a 6.1200 student would not recognize.

| Write this | Not this | Where |
|---|---|---|
| `a ≡ₙ b` | `a ≡ b (mod n)` | Lec 09 — explicitly recommended to avoid confusion |
| `n rem d`, `n div d` | `n mod d`, `n // d` | Lec 08–09 |
| `Ex[R]` | `E[R]`, `𝔼[R]` | Lec 22–24 |
| `f(n) ∈ O(g(n))` | `f(n) = O(g(n))` | Lec 06 — `=` is called "ew, but most common" |
| `ℕ` includes `0` | `ℕ` starts at 1 | Lec 01 |
| `Pr[A]`, event `[Marilyn wins]` | `P(A)` | Lec 18 |

---

## 1. Logic and proof

### Quantifiers and connectives
- `∀` universal, `∃` existential.
- Separator after the quantified variable is a **period**: `∀n ∈ ℕ. P(n)`,
  `∃x ∈ S. P(x)`. (Lec 03 occasionally uses a comma, `∀n ∈ ℕ, P(n)`; the period
  is the house default.)
- `∧` and, `∨` or (**inclusive**), `¬A` / `A̅` / "not A" for negation.
- Implication: `A ⇒ B`, `A → B`, or "A implies B" — all used interchangeably.
- `iff` (spelled out) for biconditional.
- `xor`, `nand` appear by name in the Lec 01 "waiter" discussion of how English
  "or" almost never means `∨`.

### Predicates
- A **proposition** is a statement that is either True or False.
- A **predicate** is a proposition whose truth depends on variables.
- Define with `≔`: `P(n) ≔ 1 + 2 + ⋯ + n = n(n+1)/2`.
- ⚠ A predicate is a **sentence**, not a number and not a formula. `P(n) ≔
  n(n+1)/2` is malformed — `P(3)` would be the number 6, and you cannot assume a
  6. So is `P(n) ≔ ∀n. …`, which leaves no free `n` to induct on. Both errors are
  taught explicitly (see `companions/rec-03.html` §1).

### Proof techniques and their templates
The course teaches proof *outlining* as a near-mechanical step driven by the
**shape** of the theorem, before any thinking about content. Lec 02 §4 works a
full example with `[TODO: …]` placeholders. Reproduce that habit.

| Theorem shape | Method | Opening move |
|---|---|---|
| `∃x. P(x)` | construction | "We'll show that `x = ⟨value⟩` works." |
| `∀x ∈ S. P(x)` | instantiation | "Assume `x` is an arbitrary element of `S`." |
| `P ⇒ Q` | direct | "Assume `P` is true." |
| `P ⇒ Q` | contrapositive | "We'll prove the contrapositive, so assume not `Q`." |
| `P` | contradiction | "Assume for sake of contradiction that not `P`." |
| `P` | cases | "Proof by cases on the truth value of `C`:" |
| `∀n ∈ ℕ. P(n)` | induction | "Let `P(n)` be the predicate …. We prove `∀n ∈ ℕ. P(n)` by induction on `n`." |

- Contradiction is closed with `⇒⇐` (Lec 02).
- A proof by cases must end by asserting the cases are **exhaustive**, with a
  reason.
- `WLOG` / "without loss of generality" is used freely (Lec 02 tromino, Lec 12).

### Standards for written proofs (Lec 02 §1)
Quote-worthy, because these are the actual grading standards:
- Each step should be clear and logical.
- State which previously proved propositions you are using.
- No "wild leaps of faith".
- No **"Proof by Intimidation"** (*"P is obvious"*, *"Clearly Q"*).
- But: no need to cite an inference rule at every step, and basic pre-6.1200
  math is fair game as axioms.
- "I already knew `P`, so it's an axiom" is not a proof of `P`.

### Axioms
- An **axiom** is a proposition assumed True. The course line is: *you must make
  assumptions — the key is to state them up front.*
- **Consistent**: no proposition can be both proved and disproved.
  **Complete**: every proposition can be proved or disproved.
  Gödel: no set of axioms is both.

---

## 2. Sets

- `ℕ` = **non-negative** integers `{0, 1, 2, …}`. ⚠ `0 ∈ ℕ` in this course.
- `ℤ`, `ℤ⁺`, `ℚ`, `ℝ`. Empty set `∅` or `{}`.
- `∈`, `⊆`, `∩`, `∪`; difference is `A − B` **or** `A \ B` (both used, Lec 01).
- Set-builder: `{n ∈ ℕ | isPrime(n)}`; a colon may replace the bar.
- No duplicates, order irrelevant. Ordered tuples use parentheses and allow
  both: `(6, 1, 2, 0, 0)`.
- `[n] ≔ {1, 2, …, n}` (Lec 17 appendix).
- `{0,1}ⁿ` written `Bⁿ` for the set of length-`n` bit strings (Lec 15).
- Empty operations (Lec 17 appendix): `Σ∅ = 0`, `Π∅ = 1`, `∪∅ = ∅`, `∩∅ = U`.

---

## 3. Induction

**Induction axiom** (Lec 02, Axiom 1):
> Let `P(n)` be a predicate on `n ∈ ℕ`. If `P(0)` and `∀n ∈ ℕ. P(n) ⇒ P(n+1)`,
> then `∀n ∈ ℕ. P(n)`.

**Strong induction** (Lec 03, Theorem 4) — two separate obligations:
> 1. `P(0)` is true.
> 2. `∀n ∈ ℕ. P(0) ∧ P(1) ∧ … ∧ P(n) ⇒ P(n+1)`.
>
> Then `∀n ∈ ℕ. P(n)`.

⚠ **Use the conjunction form, matching lecture.** Write the hypothesis as
`P(0) ∧ P(1) ∧ … ∧ P(n)` and the target as `P(n+1)`. Do **not** substitute the
`∀m < n` phrasing — it is equivalent, but it is not what students have in their
notes, and the re-indexing (proving `P(n)` instead of `P(n+1)`) causes more
confusion than the extra precision buys.

Note that in this formulation the **base case is a separate obligation**. It does
not fall out of the step; `P(0)` is condition 1 and you owe it independently,
exactly as in ordinary induction.

The one thing worth flagging to students: **read the dots at the smallest `n`.**
At `n = 0` the chain `P(0) ∧ … ∧ P(n)` collapses to the single term `P(0)`, so
the step is just `P(0) ⇒ P(1)`. The `…` is suggestive, not literal — it stands
for however many cases actually exist below the one being proved.

Vocabulary: **base case**, **inductive step**, **induction hypothesis (IH)**.
Base case need not be 0 (Lec 03 uses `n = 1` and calls the choice "purely
cosmetic").

**Strengthening the IH** (Lec 02 §5.3) — a signature course move:
> "When doing a proof by induction, if at first you don't succeed, try something
> harder."

The canonical examples are the `2ⁿ × 2ⁿ` L-tromino tiling (prove the stronger
"any `2²ⁿ − 1` squares" claim) and the halving sum (prove `= 1 − 1/2ⁿ`, not
`< 1`). Strong and ordinary induction are **equivalent in power** (Lec 03) —
never claim strong induction proves more.

**Buildup error** ⚠ (Lec 11 §2.5) — the named, course-specific failure mode for
induction on graphs. `P(n+1)` usually begins "for all graphs with `n+1`
vertices", so the step must open **"suppose `G` is any graph with `n+1`
vertices"** and then shrink it. The error is to start from an `n`-vertex graph
and "build up" by adding a vertex, which only reaches the graphs your
construction happens to produce. Lec 13 flags the same trap when pruning a leaf
from a tree. Treat this as a first-class concept, not an aside.

---

## 4. State machines (Lec 04)

- Transitions written `s ↦ t` (also `s → t`).
- **Preserved predicate**: `P(s)` and `s ↦ t` implies `P(t)`.
- **Invariant**: true for all reachable states.
- **Invariant Principle**: preserved + true initially ⇒ invariant.
- **Derived variable** (aka **potential function**): states → ℝ. Strictly /
  weakly decreasing. A strictly decreasing ℕ-valued derived variable proves
  **termination**.
- **Partial correctness** = "correct *if* it terminates" — the two are proved
  separately.
- Digraphs are later revealed to be what state machines were all along (Lec 14).

---

## 5. Sums, asymptotics, recurrences

### Sums (Lec 05)
- **Closed form** = "a formula you could enter into an arithmetic calculator,
  with no summations, ellipses, or recursions."
- Empty sum is `0` by convention.
- Methods, by name: **Guess and Check** (guess the closed form, prove by
  induction — "the hard part is guessing, not proving"), **Perturbation**
  (compare `S` to `xS`), **Ansatz / Educated Guessing** (posit a degree-`d`
  polynomial, solve for coefficients, *then* verify by induction).
- Geometric: `Σ_{k=0}^{n−1} xᵏ = (1 − xⁿ)/(1 − x)`; infinite `= 1/(1−x)` for `|x| < 1`.
- **Integral Method / Integral Bound** — ⚠ the course says explicitly: *"if we
  ask you to use the Integral Method, you should simply cite one of the above
  theorems. You do not need to rederive them!"* Three theorems: increasing,
  decreasing, improper.
- `Hₙ` = nth harmonic number, `Hₙ ∼ ln n`.

### Asymptotics (Lec 06)
- `f(n) ∼ g(n)` iff `lim f/g = 1`. "Equal except for lower-order terms."
- `f(n) ∈ O(g(n))` ≔ `∃c > 0. ∃n₀ ≥ 0. ∀n ≥ n₀. |f(n)| ≤ c·g(n)`.
- ⚠ Notation preference, stated outright: `f ∈ O(g)` **[preferred]**,
  `f ≤ O(g)` [also good], `f = O(g)` **[ew, but most common]**, `f "is" O(g)` [ok].
- `Ω` (`f ≥ Ω(g)`), `Θ` (both), `o` (`lim = 0`), `ω` (`lim = ∞`).
- `f ∼ f + h` iff `h ∈ o(f)` — this *is* the definition of "lower order term".
- ⚠ **"Induction and Asymptotics Don't Mix"** — a titled Lec 06 section with a
  `False Claim` / `Bogus Proof` that `2ⁿ = O(1)`. The error is quantifier order:
  induction proves `∀n. ∃c`, but big-O needs `∃c. ∀n`. To induct on an
  asymptotic claim you must **fix `c` and `n₀` first**.
- Stirling: `n! ∼ √(2πn) · (n/e)ⁿ`.

### Recurrences (Lec 07)
- **Plug and Chug**: substitute the recurrence into itself, find the pattern.
- **Master Theorem** for `T(n) = a·T(⌊n/b⌋) + f(n)`, `a ≥ 1`, `b > 1`, in three
  cases against `n^(log_b a)`. The course notes its **gaps** (e.g.
  `T(n) = 2T(n/2) + n log n` fits no case) and that Hanoi's `T(n) = 2T(n−1) + 1`
  is not of the right form at all.
- Running examples: Towers of Hanoi (`2ⁿ − 1`), Merge Sort
  (`n log₂ n − n + 1`), Selection/Simple Sort (`n(n−1)/2`), Binary Search,
  Karatsuba.

---

## 6. Number theory (Lec 08–10)

- **Divisibility**: `a | b` iff `∃k ∈ ℤ. ak = b`. Note `0 | 0`.
- **ILC** = *integer linear combination*, `sb + tc` for `s, t ∈ ℤ`. Abbreviated
  `ILC` or `i.l.c.` in the notes; a genuinely course-specific abbreviation.
- **Division Theorem**: for `d > 0`, unique `q, r` with `n = qd + r`, `0 ≤ r < d`.
  ⚠ Written **`n div d`** (quotient) and **`n rem d`** (remainder), also
  `rem(n, d)`. **Never** `n mod d` as an operator.
  - `a rem n` is **always non-negative**, even for negative `a`:
    `(−43) rem 10 = 7`. Lec 09 §3.1 catalogues which languages agree (Python,
    Mathematica) and which don't (JS, C/C++). Integer division always rounds
    **down**.
- **Congruence** ⚠: **`a ≡ₙ b`**, read "a is congruent to b mod n", defined as
  `n | a − b`. The notes acknowledge `a ≡ b (mod n)` is more standard but
  recommend the subscript form "until you are familiar with modular arithmetic",
  because `a = b mod n` is genuinely ambiguous between `a ≡ₙ b` and
  `a = (b rem n)`.
  - Keep the distinction sharp: `a rem n` is a **function** with one value in
    `[0, n)`; `a ≡ₙ b` is a **relation**. `12 ≡₅ 17` but `12 ≠ (17 rem 5)`.
- **gcd**: defined so that `gcd(0,0) = 0` and every common divisor divides it.
- **Euclid's Algorithm**; **Extended Euclidean Algorithm** ⚠ *"aka **The
  Pulverizer**"* — the course consistently uses the nickname (from Sanskrit
  *Kuṭṭaka*, Āryabhaṭa ~500 CE). State it as a 6-tuple state machine with three
  invariants.
- **Bezout's Identity**: `gcd(a,b) = as + bt`. Corollary: the ILCs of `a, b` are
  exactly the multiples of `gcd(a,b)`.
- Inverses: `x⁻¹` exists mod `n` iff `gcd(a, n) = 1`.
- **Fermat's Little Theorem**: `p` prime, `a ≢ₚ 0` ⇒ `a^(p−1) ≡ₚ 1`.
- **CRT**, RSA (`kp = (n, e)`, `ks = (n, d)`), Diffie-Hellman, one-time pad.
  Alice / Bob / **Eve the Eavesdropper** are the standing cast.
- ⚠ Exponents may **not** be reduced mod `n` — bases may. This warning is
  repeated; keep it.
- Lec 10 §2 (crypto history) is explicitly marked **NOT EXAMINED**.

---

## 7. Graphs (Lec 11–14)

### Simple graphs
- `G = (V, E)`, `V` **non-empty**, `E` a set of **2-element subsets**.
  ⚠ The course's definition **disallows** `V = ∅`, self-loops, and multi-edges,
  and says so, noting other sources differ.
- Edge `{u, v}`, also written `u − v` or `uv`. **Adjacent**, **incident**,
  **endpoints**, `deg(v)`, degree sequence.
- **Handshake Lemma**: `Σ_{v∈V} deg(v) = 2|E|`.
- **Bipartite**: `V` partitions into `L`, `R` with every edge crossing. The
  average-degree ratio `A_L / A_R = |R| / |L|` is used to debunk survey results —
  a signature example.
- `Kₙ` complete graph, `K_{1,k}` star `Sₖ`, crown graph `H_{k,k}`.

### Coloring
- **Proper k-coloring**: `f : V → C`, `|C| ≤ k`, adjacent vertices differ.
- **Chromatic number `χ(G)`** — the minimum such `k`. ⚠ Proving `χ(G) = k`
  requires **both** an upper bound (exhibit a coloring) and a lower bound (show
  `k−1` is impossible). The lectures stress this.
- **Basic algorithm** = greedy in vertex order; uses `≤ d+1` colors for max
  degree `d`. Order matters enormously.

### Matching (Lec 12)
- **Matching**, **maximal** (not extendable) vs **maximum** (largest) — the
  distinction is made explicitly. **Perfect** = `|V|/2` edges.
- **Stable Matching**: **Applicants** and **Evaluators** (the course's neutral
  terms — prefer them over "men/women" or "suitors"), **rogue couple**,
  **stable**.
- **Gale-Shapley** (aka Propose-and-Reject, Deferred Acceptance). Proved via
  state machine: terminates by day `N² + 1`, matches everyone, no rogue couples.
- **Feasible**, **optimal**, **pessimal** matches. Applicants get optimal,
  Evaluators get pessimal.

### Connectivity and trees (Lec 13)
- ⚠ **walk ⊃ trail ⊃ path** — a strict hierarchy the course is careful about:
  a **walk** follows edges (anything goes); a **trail** doesn't repeat *edges*;
  a **path** doesn't repeat *vertices*. Length = number of **edges**.
- **Connected** (a walk exists) is weaker than **adjacent** (share an edge).
  Every vertex is connected to itself by the length-0 walk.
- **Closed** walk; **tour** = closed trail; **cycle** = tour of positive length,
  no repeats. Undirected cycles need length ≥ 3.
- **Eulerian** tour / **semi-Eulerian** trail. ⚠ The lecture warns the
  terminology is a minefield ("an Euler cycle is not necessarily a cycle") —
  worth passing on rather than smoothing over.
- **Tree** = connected and acyclic. **Leaf** = degree-1 vertex. Every tree with
  `n ≥ 2` has ≥ 2 leaves. A tree has exactly `n − 1` edges. **Forest** =
  acyclic graph.
- ⚠ The standard tree induction is **prune a leaf, apply the IH, put it back** —
  and the notes point out you must remove a *leaf*, not an arbitrary vertex.

### Digraphs and DAGs (Lec 14)
- `E ⊆ V × V`, edge `(u, v)` drawn `u → v`. Self-loops and antiparallel edges
  **allowed**; parallel edges still not. ⚠ Never mix directed and undirected
  edges in one graph.
- `deg⁻(v)` / `degᵢₙ(v)`, `deg⁺(v)` / `degₒᵤₜ(v)`. No combined "degree".
- Directed cycles may have length 1 (self-loop) or 2 (antiparallel).
- **Reachable**, **strongly connected**, **SCC** written `[v]`, **condensation
  graph** (always a DAG).
- **DAG**, **source**/**sink** = **minimal**/**maximal** element, **covering
  edge** vs redundant, **Hasse diagram**, **topological order**.
- **Chain** (pairwise comparable), **antichain** (pairwise incomparable),
  **critical path** = maximum-size chain. ⚠ A critical path is a *set of
  vertices*; its **size** is a vertex count, off by one from a path's *length*.
  The lecture flags this explicitly.
- Shortest parallel schedule **equals** the longest chain. Dilworth's theorem is
  marked **not examined**.

---

## 8. Relations (Lec 15)

- `R ⊆ A × B` with a **domain** `A` and **codomain** `B`. Write `a R b` or
  `R(a, b)`.
- The four arrow properties, taught as arrow counts — memorize the phrasing:
  - **function**: "≤ 1 arrow out" of each `a`
  - **total**: "≥ 1 arrow out" of each `a`
  - **injective**: "≤ 1 arrow in" to each `b`
  - **surjective**: "≥ 1 arrow in" to each `b`
- **Bijection** = total + injective + surjective.
- Size comparisons: total injection ⇒ `|A| ≤ |B|`; surjective function ⇒
  `|A| ≥ |B|`; bijection ⇒ `|A| = |B|`.
- ⚠ "Partial does not mean 'not total'" — total functions *are* partial
  functions. The notes make this point wryly ("Naming things is hard…").
- **Equivalence relation** = reflexive + symmetric + transitive ⇒ partitions `A`
  into **equivalence classes**.
- **Weak partial order (WPO)** = reflexive + **antisymmetric** + transitive.
  A **linear / total ordering** additionally has every pair comparable.
- The walk relation on `G` is a WPO iff `G` is a DAG.

---

## 9. Counting (Lec 15–17)

The four rules, always by name:
- **Product rule**: `|A₁ × ⋯ × Aₙ| = |A₁| ⋯ |Aₙ|` — use for *and*.
- **Sum rule**: pairwise disjoint ⇒ sizes add — use for *or*.
- **Bijection rule**: a bijection ⇒ equal sizes.
- **Division rule**: a `k`-to-1 correspondence ⇒ `|B| = |A|/k`.
- **Generalized product rule**: `|A| = n₁ ⋯ n_k` when the *number* of choices at
  each step is fixed, even though the *set* of choices varies. ⚠ The course
  hammers the distinction and gives a negative example (increasing serials)
  where it fails.

- `n!` permutations; `C(n, r) = n!/((n−r)! r!)` written `(n choose r)` and read
  aloud as "n choose r".
- ⚠ **Counting by recipe** is the course's framing: describe a sequence of
  choices building your objects, then verify **two** things — every recipe
  produces something in your set, and every element comes from **exactly one**
  recipe. Poker hands are the running example, including recipes that fail and
  get rescued by the division rule (or don't, when the map isn't `k`-to-1 at all).
- **PIE** (Principle of Inclusion-Exclusion), **Pigeonhole Principle** and its
  **generalized** form (`|A| > k|B|` ⇒ some `b` has `k+1` preimages).
  Pigeonhole is **nonconstructive** — the notes stress this.
- **Combinatorial proof / double counting**: count one set two ways.
- **Binomial Theorem**, **Multinomial Theorem**, Pascal's Triangle identity
  `C(n,k) = C(n−1,k−1) + C(n−1,k)` — proved combinatorially, "by algebra using
  factorials, but no intuition" being the anti-pattern.
- **Bookkeeper rule** — the generalization of `n choose r`; taught in recitation.

---

## 10. Probability (Lec 18–24)

### Spaces and events
- **Discrete probability space** `(S, Pr)`: `S` non-empty countable **sample
  space**, `Pr : S → [0,1]` total with `Σ_{ω∈S} Pr[ω] = 1`.
- **Outcome** `ω ∈ S`. **Event** `A ⊆ S`. `Pr[A] ≔ Σ_{ω∈A} Pr[ω]`.
- ⚠ Square brackets throughout: `Pr[ω]`, `Pr[A]`, `Pr[A | B]`, `Ex[R]`, `Var[R]`.
- ⚠ Events named in brackets: `[Marilyn wins]`, `[Red wins]`, `[R = 2]`. This is
  a notation the lectures introduce deliberately — "`[X]` means the event (set of
  outcomes) in which `X` occurs".
- **Uniform** space ⇒ `Pr[E] = |E|/|S|`, so counting tools apply.

### The Four Step Method / Tree Method ⚠
The course's central procedure for probability problems, and the structure
material should follow:
0. **The question** — state the modelling axioms; they are choices, and
   different reasonable axioms give different answers (Monty Hall is the case
   study).
1. **Sample space** — build a tree; each level is a step; **outcomes are the
   leaves**.
2. **Probability function** — label edges (these are conditional probabilities);
   multiply along root-to-leaf paths.
3. **Events** — identify the subsets.
4. **Answer** — sum.

> "Throw away intuition, and simply fall back to rigorous, step-by-step
> analysis." — Lec 18

⚠ **Identify the probability space first, always.** The Lec 18 §4 warning shows
a "count successes / count total" calculation that silently mixes an unordered
numerator with an ordered denominator. Don't mix and match.

Running examples: Monty Hall, **intransitive (strange) dice**, tournaments,
biased/fair coins, COVID base rates, Simpson's paradox, the jelly-tart/O.J. prior.

### Rules
Sum rule, complement, difference, PIE, **union bound**, monotonicity — all
stated for `Pr`.
- **Conditional probability**: `Pr[A | B] = Pr[A ∩ B] / Pr[B]`.
- **Product rule**: `Pr[A ∩ B] = Pr[A | B] Pr[B]` — this is what justifies the
  tree method.
- **Bayes' rule**: `Pr[B | A] = Pr[A | B] Pr[B] / Pr[A]`. Vocabulary:
  **likelihood**, **prior**, **posterior**. The lectures lean on the **odds
  form** `Pr[B|A]/Pr[C|A] = (Pr[A|B]Pr[B])/(Pr[A|C]Pr[C])` for worked examples.

### Independence
- `Pr[A ∩ B] = Pr[A]·Pr[B]`, or `Pr[A | B] = Pr[A]`.
- **Mutual** independence needs the all-way product **too** — the three-coin
  parity example shows pairwise does not imply mutual.
- **Pairwise** independence is called out as "often a good enough substitute …
  and much easier to achieve."
- **Conditional independence**; conditioning can *create* dependence between
  causally unrelated events.
- **Gambler's fallacy**; the **Birthday Principle** (`d ≈ √n`, 23 for 365).

### Random variables
- ⚠ An **RV is a total function on the sample space** — "an event is a set, an
  RV is a function". The lectures repeat this.
- **Indicator** RV (0/1), also called **Bernoulli**; `I_A` or `1[A]`.
- Events from RVs: `[f = x]`, `[f ≥ x]`, `[f ∈ T]`.
- `PMF_X(x) = Pr[X = x]`, `CDF_X(x) = Pr[X ≤ x]`.
- Independence of RVs quantifies over **all** value pairs.
- **Binomial** `f_{n,p}(k) = C(n,k) p^k (1−p)^{n−k}`.

### Expectation ⚠
- **`Ex[R]`** — the course's spelling, not `E[R]`.
  `Ex[R] ≔ Σ_{ω∈S} R(ω) Pr[ω]`.
- Alternate: `Ex[R] = Σ_{x ∈ range(R)} x · Pr[R = x]`.
- `Ex[I_A] = Pr[A]`.
- **Linearity of expectation**: `Ex[R₁ + R₂] = Ex[R₁] + Ex[R₂]`, **no
  independence required** — the course calls it "a formidable tool in our
  arsenal" and returns to it constantly (cellphone check, lazy susan).
- ⚠ Lec 22 §6 explicitly warns these three formulas get confused or merged.
  Know which you are using.
- `Ex[R₁R₂] = Ex[R₁]Ex[R₂]` **only if independent**. `Ex[aR + b] = a Ex[R] + b`.
- ⚠ `Ex[1/R] ≠ 1/Ex[R]`, and **averaging ratios is a fallacy** — the RISC/Z8002
  benchmark table (where the same argument "proves" each is more verbose than
  the other) is the course's worked cautionary tale.
- Expectations can be **infinite**.

### Variance and tail bounds
- `Var[R] = Ex[(R − Ex[R])²] = Ex[R²] − Ex[R]²`. **`σ(R)`** = standard deviation.
- Variances of **pairwise independent** RVs add. ⚠ Standard deviations do not.
- **Markov**: `R ≥ 0` ⇒ `Pr[R ≥ x] ≤ Ex[R]/x`; alternate
  `Pr[R ≥ c·Ex[R]] ≤ 1/c`.
  - ⚠ **Adjusting bounds** is taught as a named strategy: if `S ≥ ℓ` apply
    Markov to `S − ℓ`; if `S ≤ u` apply it to `u − S`.
  - Non-negativity is required, and the notes show exactly where the proof
    breaks without it.
- **Chebyshev**: `Pr[|R − Ex[R]| ≥ x] ≤ Var[R]/x²`; any RV, sign-free.
- **Chernoff**: mutually independent `Tᵢ ∈ [0,1]`, `T = ΣTᵢ`, `c ≥ 1` ⇒
  `Pr[T ≥ c·Ex[T]] ≤ e^{−(c ln c − c + 1)·Ex[T]}`.
- The three are taught as a ladder on the same running example (`n` coin flips,
  `Pr[R ≥ 3n/4]`): Markov `2/3`, Chebyshev `4/n`, Chernoff `e^{−n/20}`. Reuse
  that ladder — it is how the course makes the bounds mean something.

---

## 11. Typography for HTML companions

The companions render math as **Unicode in styled spans**, not LaTeX/MathJax.
See `companions/rec-03.html`.

- `<span class="m">n</span>` — single italic variable (serif italic).
- `<span class="mm">…</span>` — upright serif for a longer expression.
- Both use `"Iowan Old Style", Palatino, Georgia, serif`.
- Variables are **always** wrapped: `<span class="m">P</span>(<span
  class="m">n</span>)`. It is verbose; it is also what makes the prose look like
  mathematics rather than code.
- Unicode to have on hand:
  `∀ ∃ ∈ ∉ ⊆ ⊂ ∪ ∩ ∅ ≤ ≥ ≠ ≡ ≔ ⇒ ⇔ ∧ ∨ ¬ Σ Π √ ∞ ⌊ ⌋ ⌈ ⌉ ℕ ℤ ℚ ℝ χ σ ω Ω Θ ϕ ↦ → ⇒⇐`
- Subscripts/superscripts inline: `≡ₙ`, `2ⁿ`, `n²`, `Hₙ`, `deg⁻`, `x₀`. Use real
  Unicode sub/superscripts in prose; use `<sup>`/`<sub>` when the character
  doesn't exist.
- Escape `<` as `&lt;` — it appears constantly in `m &lt; n`.
