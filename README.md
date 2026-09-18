# 61200

Pedagogical tools and companions for **6.1200J / 18.062J — Mathematics for
Computer Science** (MIT, Fall 2026).

Interactive review pages for recitations, plus the reference material that keeps
them faithful to the course's notation, vocabulary, and examples.

## Companions

Each is a single self-contained HTML file — no build step, no dependencies
beyond a webfont. Open one in a browser.

| Recitation | Topic |
|---|---|
| 03 | [Strong induction — predicates, ordinary vs. strong, strengthening](companions/rec-03.html) |

## Reference

- [`course/NOTATION.md`](course/NOTATION.md) — the course's notation and
  conventions, with the places it diverges from textbook default marked
- [`course/COURSE-MAP.md`](course/COURSE-MAP.md) — all 24 lectures, what each
  covers, recitation pairings, course logistics
- [`course/VOICE.md`](course/VOICE.md) — how companions are written and what
  makes an interactive widget worth building
- [`course/PITFALLS.md`](course/PITFALLS.md) — mistakes the course names, from
  *proof by example* to *buildup error* to *the ratio fallacy*

## Lecture PDFs

`lectures/` holds the source notes. It is gitignored — the PDFs are ~25 MB of
staff course material and don't belong in version control. Drop them in locally
to give the tools something to read.

## Working on this repo

See [`CLAUDE.md`](CLAUDE.md). Three skills live in `.claude/skills/`:
`recitation-companion` (build a companion), `concept-explainer` (explain a
concept in the course's terms), `proof-feedback` (critique a proof against the
course's stated standards).
