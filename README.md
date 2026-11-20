# The Civics Facts

A minimalist study tool for the U.S. naturalization civics test.

**[Read the case study →](CASE_STUDY.md)** · how I turned a static question list into a learning system

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

All 128 official questions are covered by 124 cards. Four pairs of
questions share the same answer, so each pair is taught as one fact.
Each card has a row of icons that spells out the answer.

## Try it

**[Open the app](https://juliaweikel.fyi/civics-app/)**, or open `civics_book_prototype.html` in a browser. Start from the
cover page, pick a chapter, and read.

## Project structure

```
civics-mnemonic-app/
├── README.md
├── CASE_STUDY.md                # portfolio case study
├── PROCESS.md                   # how it was built
├── PRODUCT_BRIEF.md             # design document
├── civics_book_prototype.html   # the app
├── index.html                   # redirects to the app
├── facts_*.json                 # curated facts, by category
└── *clusters*.json              # fact groupings
```

## Tech

Single self-contained HTML file. No build step, no dependencies. Study
progress is saved locally in the browser between visits.

## License

TBD
