# 6.1200 Pedagogical Tools

Teaching material for **6.1200J / 18.062J, Mathematics for Computer Science**
(MIT, Fall 2026). Interactive companions, explanations, and proof feedback that
match the course's own notation, vocabulary, and examples.

## Before writing any course content

Read [`course/NOTATION.md`](course/NOTATION.md). The §0 table is the short
version — six places where the ordinary habit produces something a 6.1200
student would not recognize:

| Write | Not |
|---|---|
| `a ≡ₙ b` | `a ≡ b (mod n)` |
| `n rem d`, `n div d` | `n mod d` |
| `Ex[R]` | `E[R]` |
| `f(n) ∈ O(g(n))` | `f(n) = O(g(n))` |
| `ℕ` contains `0` | `ℕ` starts at 1 |
| `Pr[A]`, `[Red wins]` | `P(A)` |

Getting notation wrong is worse than being vague. A student reading unfamiliar
symbols concludes their notes are wrong.

## Layout

```
course/          Reference material — read these, don't guess
  NOTATION.md      Authoritative notation and conventions, unit by unit
  COURSE-MAP.md    All 24 lectures: content, recitation pairings, logistics
  VOICE.md         Register, companion structure, interactivity standards
  PITFALLS.md      Errors the course names — buildup error, ratio fallacy, …
companions/      Built artifacts, one self-contained HTML file each
lectures/        Source PDFs — present locally, gitignored (~25 MB, staff material)
.claude/skills/  Task-specific skills
```

## Companions

One self-contained HTML file per companion, named by what it accompanies — the
number only, no topic slug:

| File | For | Published at |
|---|---|---|
| `companions/rec-03.html` | Recitation 03 — strong induction | — |
| `companions/lec-04.html` | Lecture 04 — state machines, via tic-tac-toe | https://claude.ai/artifact/Gw4pLqrRhrVGznhiZzbJGL |

- `rec-NN.html` for a recitation, `lec-NN.html` for a lecture topic. Two digits.
- Footer matches the file: `a short companion to Recitation NN` or `… to Lecture NN, <topic>`.
- When adding one, add a row here, in the `README.md` table, and in the table at
  the bottom of `course/COURSE-MAP.md`.
- When editing one that has been published, republish to its existing URL
  rather than creating a new artifact, so shared links keep working.

`lec-04.html` settled a few conventions worth reusing for later state-machine
material: a state is written `(b, p)` with the board as a 3×3 tuple and `–` for
an empty cell (not `·`); cells are addressed `(row, col)`; a state with no
outgoing transitions is a **final state** (not "stuck" or "terminal"); and the
termination argument is phrased as a **potential function** (also called a
derived variable), laid out as define / strictly decreases / conclude.

## Skills

| Skill | Use it for |
|---|---|
| `recitation-companion` | Building an interactive HTML companion for a recitation or topic |
| `concept-explainer` | Explaining a concept in the course's own terms, conversationally |
| `proof-feedback` | Critiquing a student's proof against the course's stated standards |

## Working with lectures

The PDFs are gitignored but should be present at `lectures/`. Extract text
rather than reading PDFs directly — it's far cheaper and the layout survives:

```bash
pdftotext -layout lectures/lec03-strong-induction.pdf -
```

Files are `lec01-proofs.pdf` through `lec24-tail-bounds.pdf`.

## Standing rules

**Don't invent course content.** If you don't know whether 6.1200 uses a term or
states a theorem a particular way, check `NOTATION.md`, then the lecture text.

**Reuse the course's examples.** Die Hard water jugs, the block-splitting game,
intransitive dice, the cellphone check, the exam-scheduling graph made of MIT
course numbers. A callback to something a student has already seen is free.

**Match lecture's notation, then teach the careful reading.** Don't substitute a
cleaner formulation for a loose one — students end up holding two incompatible
versions. Strong induction is the standing example: use lecture's
`P(0) ∧ P(1) ∧ … ∧ P(n) ⇒ P(n+1)`, not `∀m < n`, and spend the words on what the
dots mean at `n = 0` instead.

**No pset solutions.** The collaboration policy requires students to write up
alone, without reference to outside solutions, explicitly including AI. Explain
techniques, build companions, critique work they've written, give worked
analogues. Don't produce something submittable. See
[`course/VOICE.md §6`](course/VOICE.md).
