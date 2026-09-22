---
name: recitation-companion
description: Build a post-recitation interactive HTML companion for 6.1200 (Mathematics for Computer Science). Use when asked to make a companion, handout, review page, or interactive explainer for a 6.1200 recitation or lecture topic — e.g. "make a companion for recitation 7", "build something for the Pulverizer", "students are stuck on buildup error".
---

# Building a 6.1200 Recitation Companion

A companion is a **single self-contained HTML file** that a student reads after
recitation, when they have already argued the problem at the board and something
still isn't sitting right. It is short, interactive, and opinionated about what
actually decides whether a proof works.

**The reference implementation is
[`companions/rec-03.html`](../../../companions/rec-03.html).**
Read it before writing a new one. It is the spec.

## Read first

| File | Why |
|---|---|
| [`course/NOTATION.md`](../../../course/NOTATION.md) | Non-negotiable. `≡ₙ`, `rem`, `Ex[R]`, `∈ O(·)`, and the `.m`/`.mm` span convention. |
| [`course/VOICE.md`](../../../course/VOICE.md) | Register, section shape, what makes a widget worth building. |
| [`course/PITFALLS.md`](../../../course/PITFALLS.md) | The named errors. A companion usually exists because of one of these. |
| [`course/COURSE-MAP.md`](../../../course/COURSE-MAP.md) | What that recitation covered and which lecture it follows. |
| `lectures/lecNN-*.pdf` | The source of truth. Gitignored but present locally. |

Lecture PDFs are text-extractable — `pdftotext -layout lectures/lec03-*.pdf -`
is much cheaper than reading the PDF directly.

## Process

### 1. Find the real confusion
Ask, or infer from the request, **what went wrong at the board**. A companion
built around a topic is flat; one built around a specific misunderstanding has a
spine. `rec-03.html` exists because students wrote
`P(0), P(1), …, P(n−1)` and lost track of what that means at `n = 1`.

If you genuinely don't know, ask. One question, then build.

### 2. Pick three claims
Three sections, four at most. Each heading is a **claim, not a topic**:

- ✅ `A predicate is a sentence`
- ✅ `Sometimes you have to claim more`
- ❌ `Predicates` / `Strengthening the hypothesis`

Order them so each one is needed by the next.

### 3. Design one widget per claim
For each section ask: *what could the reader manipulate such that the claim
becomes undeniable?* The highest-value pattern is the **contrast toggle** —
same example, flip between the version that works and the one that doesn't.

Working patterns from the reference file, all reusable:

| Pattern | Mechanic | Good for |
|---|---|---|
| **Instantiator** | pick an object + pick `n` → render the resulting sentence | making an abstraction concrete |
| **Triage** | judge candidates good/bad, get feedback per item | recognizing well-formed vs malformed |
| **Slot viewer** | toggle a mode, see which facts you hold vs must prove | "what am I allowed to assume?" |
| **Step-through** | Next-line button that advances a derivation, with restart | showing *where* an argument breaks |
| **Slider + visual** | drag a parameter, watch a quantity/gap respond | limits, sums, growth, bounds |
| **Quick check** | MCQ with distractors that encode real misconceptions | consolidating a section |

If a static sentence would do the same job, **write the sentence**.

### 4. Write it
Copy the reference file's `<style>` block verbatim — the token system, dark-mode
triples, and component classes are already right. Then replace the body and the
script.

Skeleton:

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Short evocative title</title>
<!-- Google Fonts: Bricolage Grotesque + JetBrains Mono + Public Sans -->
<style>/* copied from the reference companion */</style>

<header class="hero">
  <div class="wrap">
    <div class="kicker">6.1200 · after Recitation NN</div>
    <h1>A claim, not a topic</h1>
    <p class="sub">One sentence that names the gap and promises compression.</p>
  </div>
</header>

<section id="s1">
  <div class="wrap">
    <div class="shead"><span class="snum">1</span><h2>First claim</h2></div>
    <p>Two or three sentences of prose.</p>

    <div class="card">
      <span class="tag">Try it</span>
      <h4>An instruction, not a label.</h4>
      <div class="row"><div class="seg" id="…"></div></div>
      <div class="out" id="…"></div>
      <div class="expl" id="…"></div>
    </div>

    <div class="note">The observation the widget was built to produce.</div>
  </div>
  <div class="wrap"><hr class="soft"></div>
</section>

<!-- §2, §3 … -->

<section id="s4">
  <div class="wrap">
    <div class="take">
      <h3 style="font-size:19px">The short version</h3>
      <ol>
        <li><strong>Imperative takeaway.</strong> One sentence of why.</li>
      </ol>
    </div>
  </div>
</section>

<footer>
  <div class="wrap">6.1200J / 18.062J · a short companion to Recitation NN, Fall 2026.</div>
</footer>

<script>(function(){ "use strict"; /* one IIFE block per widget */ })();</script>
```

Class vocabulary already defined in the stylesheet:

- Layout — `.wrap` `.hero` `.kicker` `.sub` `.shead` `.snum` `hr.soft`
- Content — `.card` `.tag` `.note` `.note.warnb` `.note.okb` `.take`
- Controls — `.row` `.seg` `.nbtn` `.btn` `.btn.pri` `.opt`
- Output — `.out` `.expl` `.verdict.T` `.verdict.F` `.fb`
- Judgement UI — `.tcard` `.cand` `.tbtn` `.tbtn.ok` `.tbtn.no` `.tfb.g` `.tfb.b`
- State display — `.slots` `.slot.have` `.slot.goal` `.slot.none`
- Comparison — `.pair` `.vcard.yes` `.vcard.no`
- Math — `.m` (italic variable) `.mm` (upright expression)

### 5. Check it
Open it and actually click things:

```bash
open companions/rec-NN.html
```

- [ ] Every notation claim matches `NOTATION.md`.
- [ ] Every widget responds; no console errors.
- [ ] Light **and** dark both legible (toggle your OS setting).
- [ ] Readable at 375px wide, no horizontal scroll.
- [ ] `<` is escaped as `&lt;` everywhere — this bites constantly with `m &lt; n`.
- [ ] Variables wrapped in `<span class="m">`, not left bare.
- [ ] Footer says the right recitation number.
- [ ] Add a row to the table at the bottom of `COURSE-MAP.md`.

Save as `companions/rec-NN.html`, matching the recitation number — or `companions/lec-NN.html` when the
companion is built for a lecture topic rather than a recitation. Two-digit number, nothing else in the name.

## Rules

**Don't invent course content.** If unsure whether 6.1200 uses a term, check
`NOTATION.md`, then the lecture text. Unfamiliar-but-correct notation makes
students doubt their own notes.

**Reuse the course's examples.** Chocolate bars, Die Hard jugs, intransitive
dice, the cellphone check. A callback to something they've already seen is free
pedagogical leverage.

**Bogus proofs are native here.** `False Claim.` / `Bogus Proof.` /
"Where's the error?" is a device the lectures use deliberately (Lec 06, Lec 23).
A step-through widget over a bogus proof is a strong companion centerpiece.

**Match lecture's notation; don't substitute a cleaner one.** If a lecture
formulation is loose, keep it and teach the careful reading — a companion that
introduces rival notation leaves students holding two versions. `rec-03.html`
uses lecture's `P(0) ∧ P(1) ∧ … ∧ P(n) ⇒ P(n+1)` rather than the equivalent
`∀m < n`, and spends its ink on what the dots mean at `n = 0`.

**Don't produce pset solutions.** See `VOICE.md §6`.
