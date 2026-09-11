# The Civics Facts

A minimalist study method for the U.S. naturalization civics test,
built from my own experience preparing for it.

## The idea

Most civics test prep is a flashcard quiz: a question appears, you try
to recall the answer, you check if you were right. That format works
for some material. For this material — 128 dense, dry facts, studied
under real anxiety — I don't think it does.

This project tests a different hypothesis: that plain, repeated
exposure to a fact, stripped of quiz pressure and stripped of noise,
sticks better than being tested on it. So instead of a quiz, this is a
short book. Each page states one fact plainly, paired with a simple
visual cue. You read it. You read it again tomorrow. There's no score.

The content design follows the same principle. Where the official test
accepts several correct answers to one question, this project picks
one — the shortest, clearest, least confusable option — rather than
presenting all of them at once. Multiple acceptable answers made sense
as a quiz feature; they were noise for a book. The generation process
for this project is documented in `PROCESS.md`.

## Status

61 of 128 official questions are fully worked through and readable in
the prototype. This is a working prototype, not a finished product —
that distinction is intentional, not a hedge.

## Try it

Open `prototype/civics_book_prototype.html`. Start from the cover page,
pick a chapter, and read.

## What's in this repo

This started as a personal side project — a way to prepare for my own
citizenship interview — and turned into something worth documenting
properly. The two process documents below aren't required reading to
use the tool, but they're the more interesting part of the repo if
you're evaluating how it was built rather than just using it:

- **`PRODUCT_BRIEF.md`** — the working design document: audience,
  positioning, the data model, and the decision frameworks used to
  curate each fact and choose its memory technique.
- **`PROCESS.md`** — a running build log, including the wrong turns:
  an early quiz-based prototype that got scrapped, a mislabeled
  category that was corrected, and a deliberate pivot from "maximalist
  illustration" to the minimalist style the project actually shipped
  with.

Between them, this ended up touching on product and marketing thinking
— positioning, audience definition, content strategy — more than I
expected going in. That wasn't the plan at the start; it's just where
building this honestly led.

## Project structure

```
civics-mnemonic-app/
├── README.md              # you are here
├── PROCESS.md              # build log / case study
├── PRODUCT_BRIEF.md         # design document and decision frameworks
├── prototype/
│   ├── civics_book_prototype.html   # current version — the book format
│   └── civics_prototype.html        # earlier quiz-based version, kept for the record
├── data/                   # curated facts, clusters, and entity groupings, by category
├── docs/
│   └── prompts/            # saved prompt iterations for mnemonic generation
└── src/                    # (reserved for future application code)
```

## Tech

The current prototype is a single self-contained HTML file — no build
step, no dependencies. Review progress persists locally between visits.

## License

TBD
