# Building a Civics Test Mnemonic App: A Process Log

This is a running case study of building this project — where I let an AI
tool ("vibe coding") handle things, where I wrote code myself first and had
it reviewed, what broke, and what I actually learned along the way. Entries
are dated and left in the order they happened, including the wrong turns.

---

## September 2026 — Why this project

The idea started from a deck I'd already built for myself: visual and
number associations to help pass the U.S. citizenship civics test, using
color, layout, and pop-culture wordplay instead of rote memorization. The
goal for this repo is two things at once — an actual usable study tool,
and a documented case study of building it with a mix of hand-written
decisions and AI-assisted execution, so the process is as visible as the
result.

What was genuinely uncertain going in: whether the humor/pop-culture
technique from my personal deck would generalize to anyone else, whether
"AI curates the best answer when USCIS accepts several" was even a
defensible thing to do, and what the actual interaction model should be.
All three got resolved through real back-and-forth, not decided upfront
— see below.

## Product scoping — before any code

Before touching the repo, we spent a long session on product decisions:
who the audience actually is (English-fluent, pop-culture-literate,
long-term US residents from Anglophone countries — not a broad ESL
audience for v1), which version of the civics test to target (2025,
128-question), and a real framework for two hard problems: which answer
to teach when USCIS accepts several, and which mnemonic technique fits
a given fact. That framework — distinctiveness, concreteness, brevity,
rhyme potential for answer choice; numeric badge / contrast pair /
phonetic pun / translation-metaphor / plain icon for technique choice —
became the spec everything after this was built against. See
`PRODUCT_BRIEF.md` for the full framework; it's the actual design
document, not this file.

**Skill built:** separating "what to teach" from "how to make it stick"
as two distinct curation decisions, each with its own criteria — rather
than one vague "make it memorable" step.

## Curating the pilot content — hand-designed first, AI-assisted at scale

Ran all 20 pilot facts (Geography/Symbols/Holidays + Founding Fathers)
through the framework by hand, fact by fact, rather than batch-generating
answers and hoping they were good. This caught a real mistake: an early
pass curated Thomas Jefferson's entity-hub fact as "the Louisiana
Purchase" — which turned out to duplicate a different fact (buying the
Louisiana Territory) that was *already* being taught elsewhere in the
pool. Caught only because the distinctiveness criterion was applied
consistently, not because of a name-based bug. Fixed by re-checking every
entity hub's facts against everything else already curated for that
person, not just within the current category.

**Skill built:** curation isn't a one-shot generation step — it needs a
cross-check against everything else in the corpus, or duplicate content
slips through silently.

## First build: a quiz. It was wrong.

The first working prototype was a quiz-drill loop — question shown, tap
to reveal the answer, rate your recall, spaced-repetition scheduling
decides what's due tomorrow. It worked technically (persisted state via
`window.storage`, a real SM-2-style scheduler) but it was built on an
assumption I never actually confirmed: that "study tool" meant "quiz."

It didn't. The actual mental model was a children's book — something you
read and re-read, with the facts stated plainly, not posed as questions
to be tested on. Self-testing is a mode you can switch into, not the
default way you encounter the content.

**Roadblock:** the fix wasn't a tweak to the quiz UI, it was a full
rebuild — different data presentation (statement instead of question),
different navigation model (flip through pages vs. a scored "due today"
queue), and dropping spaced-repetition scheduling entirely in favor of a
simple day-streak. Both prototype files were kept in the repo rather than
overwriting the first — the wrong version is as useful a record as the
right one.

**Skill built:** confirm the interaction model explicitly before building
it, even when the content architecture underneath is solid. Good data
doesn't guarantee the right UI sits on top of it.

## Building the icon set — from placeholder to real visual language

Once the book format was right, the placeholder colored shapes (a plain
circle standing in for "numeric badge," for example) weren't enough to
judge whether the actual mnemonic techniques worked — you can't tell if
a pun lands from a gray box. Built a real hand-drawn SVG icon set instead
— a feather, a Capitol dome, a flag that actually renders stripes vs.
stars, a crossed-out crown for the "not a president" contrast cards, a
tricorn hat standing in for Washington rather than a likeness — matching
the bold flat Americana palette from the original deck (rust, mustard,
cream, navy).

Couldn't render-test this in a browser directly — the sandbox's headless
browser install was blocked by network restrictions — so verification
was: check the JS parses cleanly, and cross-check every icon name a fact
references against the icon library to make sure nothing points at an
undefined icon and renders blank. That catches wiring bugs, not visual
quality — actual "does this read clearly" judgment still needed a human
looking at it.

**Skill built:** when you can't verify visually, verify what you can
(structural correctness) and say plainly what you couldn't check, rather
than presenting untested code as done.

## The minimalist pivot — from placeholder to deliberate MVP strategy

The original creative direction for this project was maximalist and
"unhinged" — full illustrated pop-culture poster art, in the spirit of
the founder's original deck (Jude Law standing in for "rule of law,"
George Washington set to a cartoon theme song). When it came time to
replace placeholder shapes with real icons, what got built instead was
minimalist — clean flat SVG icons, a restrained four-color palette, no
illustrated scenes. That wasn't a deliberate style decision at the
time; it was the fastest way to get something real to look at, and it
also sidestepped a real constraint (AI-generated tools won't render
likenesses of real, named people, which the original "unhinged" pun
mechanic leaned on).

The pivot: rather than treating the minimalist result as unfinished
work waiting for "real" illustration, it got reviewed honestly and kept
on purpose. "Civics memorization for minimalists" is now the stated V1
direction, not an apology for what didn't get built. The playful,
sometimes odd technique layer underneath — a tune set to a cartoon
theme, five state names grouped by a shared "New" prefix, a crossed-out
crown for "not a president" — is untouched. Only the rendering style
changed from what was originally scoped.

**Skill built:** recognizing when a practical shortcut has actually
produced the right answer, and being willing to consciously adopt it
rather than treating "what I originally planned" as the only legitimate
outcome. Not every pivot is a correction of a mistake — this one was a
correction of an assumption.

## What's still open

- Two facts (Independence Day as its own page vs. as part of "name three
  holidays") still overlap in content — not yet resolved.
- Only 20 of 128 official questions are curated so far.
- No real usage data yet — the book exists and works, but hasn't been
  used across multiple real days to see if the day-streak actually pulls
  anyone back.

## What I'd do differently

<!-- fill in once there's been real multi-day usage to reflect on -->
[fill in later]
