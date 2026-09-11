# The Civics Facts

A minimalist study tool for the U.S. naturalization civics test.

## What this is

Most civics test prep is a flashcard quiz — a question appears, you
recall the answer, you check if you were right. This is different: a
short book. Each page states one fact plainly, alongside a simple visual
cue. No score, no quiz pressure. You read a page, then the next, then
come back and read them again.

Where the official test accepts several correct answers to a question,
this tool teaches one — the clearest, most distinct option — rather than
listing every accepted variant at once.

## Status

All 128 official questions are built and readable in the prototype.
This is a complete first pass through the content — visual style and
interaction details are still being refined.

## Try it

Open `prototype/civics_book_prototype.html` in a browser. Start from the
cover page, pick a chapter, and read.

## Project structure

```
civics-mnemonic-app/
├── README.md
├── prototype/
│   ├── civics_book_prototype.html   # current version
│   └── civics_prototype.html        # earlier version, kept for reference
├── data/                            # curated facts, by category
├── PROCESS.md                       # build log
├── PRODUCT_BRIEF.md                 # design document
├── docs/
└── src/
```

## Tech

Single self-contained HTML file. No build step, no dependencies. Study
progress is saved locally in the browser between visits.

## License

TBD
