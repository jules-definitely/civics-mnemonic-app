# Product Brief: Civics Test Mnemonic App

## Positioning

**Serious learning for unserious people.**

The U.S. naturalization civics test is dry, high-stakes, and delivered as
information overload — a flat list of facts to memorize under real anxiety
(one mistake can mean re-testing, delay, or worse). This product doesn't
change the seriousness of the process or the accuracy of the content. It
changes the *encoding* — using vivid, sometimes absurd visual and verbal
hooks so facts actually stick, instead of bouncing off a tired brain doing
rote memorization the night before an interview.

## Target user (v1)

- Fluent English speaker, comfortable online
- Culturally literate in mainstream Western/Anglophone pop culture
  (film, TV, music) — not necessarily American-born; includes long-term
  immigrants from Anglophone countries (UK, Australia, NZ, Canada) who've
  lived in and absorbed American culture for years and are now
  naturalizing
- Not designed in v1 for: ESL learners, low digital literacy users, users
  who need the interface itself localized into another language

This is a deliberate narrowing, not a limitation — it lets the mnemonic
layer use specific, sharp cultural references instead of hedging toward
maximum universality. Explicitly *not* limited to Australian references —
the founder's situation (Australian, 15 years in the US, integrated into
American culture) is the model case, and the humor draws on shared
Western/American pop culture generally, not one country's references.

## Core design rule: the two-layer card

Every fact has two layers, and they carry different jobs:

1. **The plain-text canonical fact** — a short, accurate, defensible
   sentence. This is the layer you'd stand behind to an immigration
   attorney. It's always present, always literal, never sacrificed for a
   joke.
2. **The mnemonic layer** — the vivid, sometimes unhinged visual/verbal
   hook designed purely for stickiness. This layer can be as bold,
   punny, or absurd as it wants, *because it never has to carry the
   literal truth by itself.*

This is what resolves the tension between "serious, high-stakes content"
and "vibrant, unhinged design" — the accuracy lives in layer 1, the
memorability lives in layer 2, and neither has to compromise the other.

## Data model: Fact, not Question

The atomic content unit is a **Fact**, not a question-and-answer pair.
Multiple official question phrasings can point at the same fact (e.g.
"Who was the first President?" and "Who is the 'Father of Our Country'?"
both resolve to Washington). Modeling by fact avoids duplicated or
conflicting mnemonics for the same underlying knowledge.

```
Fact
├── canonical_statement        plain-text, accurate, defensible
├── linked_questions[]         official USCIS phrasings that map to this fact
├── accepted_answer_variants[] all answers USCIS would accept, if multiple
├── curated_answer             the one variant we've chosen to teach
├── curation_rationale         why this variant (distinctiveness, brevity,
│                              imageability, rhyme potential)
├── category                   theme cluster, not question-number range
├── time_sensitive: bool       true = gets an asterisk ("verify before
│                              your interview") — officeholders, current
│                              events, anything that can change
├── mnemonic_technique         which device was used and why
└── visual_treatment           asset/style used to express it
```

### Choosing the curated answer (when multiple are accepted)

Score candidate answers on:
- **Distinctiveness** — low risk of confusion with a different question's
  answer
- **Concreteness/imageability** — does it produce a mental picture
- **Brevity** — survives interview-nerves recall better
- **Rhyme/phonetic potential** — is a hook even available

### Choosing the mnemonic technique (decision framework, not a fixed style)

Not every fact should get the same treatment. Pick per fact:

| Fact shape | Technique |
|---|---|
| Hinges on a number | Numeric badge (bold number, consistent colored disc) |
| Easily confused with another fact | Contrast-pair panel (side-by-side minimal pairs) |
| A name/word sounds like something else | Phonetic/lexical pun, stylized visual (not a real likeness) |
| Narrative/sequential | Timeline treatment |
| Plain, no natural hook | Reduce to icon + 1–3 word label; don't force a gimmick |

A weak, forced pun is worse than no pun — it adds noise without adding a
strong retrieval hook.

## Sensitivity flag

Not every fact should get the "unhinged" treatment just because a pun or
gimmick is technically available. Facts touching a living culture, a
marginalized group, or a historical trauma (e.g. Native American tribes,
slavery, the civil rights movement) get a `sensitivity_flag: true` field.
Default treatment for flagged facts is plain and respectful — icon +
label, no forced wordplay. Humor is only used on flagged facts if it's
clearly and unambiguously punching in the right direction, and that's a
judgment call made deliberately per-fact, not a default.

## Additional mnemonic technique: translation/metaphor visual

Some facts aren't about a name, a number, or a date — they're about
*meaning* (e.g. "E Pluribus Unum" → "Out of many, one"). For these, the
right technique is a visual metaphor for the concept itself (e.g. many
small shapes merging into one), not a pun. Added to the technique
decision table:

| Fact shape | Technique |
|---|---|
| Hinges on a number | Numeric badge |
| Easily confused with another fact | Contrast-pair panel |
| A name/word sounds like something else | Phonetic/lexical pun, stylized visual |
| Narrative/sequential | Timeline treatment |
| About meaning/translation rather than a name/number | Translation/metaphor visual |
| Plain, no natural hook, or sensitivity-flagged | Icon + 1–3 word label, no forced gimmick |

## Clustering: two distinct mechanisms

Clustering is a *display* decision layered on top of independently
tracked Facts — merging facts visually never merges their review/mastery
state in spaced repetition. Two different clustering mechanisms exist,
with different rules:

### 1. Structural / confusability clusters

Facts that share a visual shape, or that are already at risk of being
confused with each other, are taught together on one shared image.

**Criteria:**
- Structural symmetry (same "shape" of fact — e.g. two numbers about the
  same object)
- Confusability (facts already prone to being mixed up are *better*
  studied side by side — e.g. Memorial Day / Veterans Day)
- Natural single-image capacity (a timeline, map, or diagram can hold
  several data points cleanly)
- **Hard cap: 3–4 facts per merged card.** Beyond that, the merged card
  recreates the information-overload problem the product exists to solve.

**Anti-pattern:** don't merge facts just because they share a category
tag with no shared memory mechanism (e.g. "capital of the U.S." and
"where's the Statue of Liberty" are both "places" but knowing one does
nothing to help recall the other — keep these standalone).

### 2. Entity clusters

Facts that share a *person* (or other recurring entity) rather than a
visual shape or category — e.g. multiple George Washington facts spread
across Founding Fathers, Colonial Period, and System of Government. This
works because a familiar, well-known person is itself a strong memory
hook — new facts attach to an existing rich mental file instead of being
encoded from scratch.

**Differences from structural clusters:**
- Not capped — an entity can accumulate as many linked facts as the test
  actually has for them
- Not confined to one category — facts can come from anywhere in the
  128-question pool
- Visual treatment is hub-and-spoke (one recognizable figure, individual
  fact-cards branching off) rather than one crammed shared image
- Each linked fact is still reviewed independently in spaced repetition

**Data model addition:**

```
Fact
├── ...(existing fields)
├── sensitivity_flag: bool     true = default to plain/respectful treatment
└── entity_tags[]              e.g. ["George Washington"] — independent of category
```

```
Cluster
├── type                        "structural" | "entity"
├── title                       e.g. "Flag Facts", "George Washington"
├── member_fact_ids[]           2-4 for structural; uncapped for entity
├── shared_visual_asset         one image (structural) or hub figure (entity)
└── merge_rationale             why these belong together
```

## Refinements found while curating Founding Fathers

Two things the framework didn't explicitly account for, discovered by
actually running real facts through it (not designed in the abstract):

**A Fact can belong to a structural cluster and an entity cluster at the
same time.** Franklin's "not a president" fact and Hamilton's "not a
president" fact form a structural/confusability cluster with each other
*and* each independently anchors its own entity hub. These aren't
competing memberships — `cluster_id` (structural) and `entity_tags`
(entity) are independent fields on the same Fact record.

**New technique: tune_parody.** Distinct from a phonetic/lexical pun —
this sets new lyrics to an existing, already-memorized melody (e.g. the
founder's George Washington bit set to the *George of the Jungle*
theme), rather than bridging via a sound-alike word. Constraint: the
borrowed tune must be broadly recognized within the target audience, or
the hook only works for whoever wrote it.

**Distinctiveness has to be checked against the whole pool, not just the
current fact.** An early draft curated Jefferson's entity-hub answer as
"Louisiana Purchase" — which turned out to duplicate fact 90's content
exactly. Caught and fixed by re-applying the distinctiveness criterion
across everything already curated for that person, not just within the
current category. Worth re-checking this on every future entity hub.

Pun mechanics that reference real people's names (e.g. "rule of law" /
Jude Law) are a valid technique, but execution should avoid rendering an
actual likeness of a real person — both for practical reasons (AI image
generation tools generally won't render real, named public figures) and
product-safety reasons (publicity-rights exposure varies state to state
if this is ever shown publicly). Preferred execution: stylized
silhouette + bold nameplate/typography, or invented parody-format art
that riffs on a format (movie poster, etc.) without a real face.

## Handling time-sensitive facts

Officeholder-dependent facts (President, VP, Chief Justice, Speaker of
the House, etc.) are not excluded or specially re-architected — they get
a visible asterisk/marker meaning "verify this is still current before
your interview." Simple, low-complexity, sufficient for v1.

## Test version target

Targeting the **2025 civics test**: 128 questions, up to 20 asked at
interview, 12 correct required to pass. Applies to Form N-400 filed on
or after Oct. 20, 2025. (USCIS has signaled a further redesigned test
may arrive around October 2026 — content pipeline should assume another
revision is likely, not a one-time build.)

## Chunking

Content is grouped by **theme cluster**, not sequential question-number
blocks. E.g.: Colonial era → Constitution → Branches of government →
President → Supreme Court → Congress → Rights → Civic participation →
Geography/symbols. This mirrors how the founder's original deck was
already organized and reduces cognitive load by chunking related facts
together (rather than 128 flat, isolated items).

## Retention as the success metric

Pass-rate self-reporting is assumed too unreliable to collect. Success
is instead **repeated, voluntary use** — if people come back without
being prompted, the format and content are working.

Two mechanisms drive return, and v1 should pick a primary:

1. **Spaced-repetition scheduling** — the app itself surfaces "X facts
   due for review today." Cheap to build (a scheduling function over
   existing content), return is built into the mechanic.
2. **Content novelty** — new cards, a "fact of the day," expanding
   categories. Pulls people back out of curiosity, but requires an
   ongoing content pipeline to sustain.

*Open decision: which is primary for v1 — see Open Questions.*

## Legal / trust considerations

- Clear, visible disclaimer: not affiliated with or endorsed by USCIS;
  study aid only, not legal advice; verify current officeholders and
  local information independently.
- No use of official government seals or typography that could imply
  official status.
- Content sourced from and traceable to the official USCIS question
  list; any deviation (curated answer choice, mnemonic framing) should
  be clearly separable from the canonical fact layer.
- State-specific/local-representative questions are explicitly punted
  to a "check your local information" prompt in v1 (the founder's own
  original deck already used this pattern on the official slide).

## Explicitly out of scope for v1

- ESL / non-fluent-English support, interface localization
- Low-digital-literacy accessibility work
- Ad or subscription monetization (may revisit later)
- Dynamic/live data pulls for officeholder facts (asterisk approach
  instead)
- Formal pass-rate outcome tracking

## Open questions

- [x] Primary retention mechanism for v1: **spaced repetition** (chosen —
      cheaper to build, more evidence-backed, doesn't require an ongoing
      content pipeline to sustain return visits)
- [x] Pilot category: **Geography, Symbols, and Holidays** (12 questions,
      run through the full curation + technique + clustering framework —
      see `data/facts_geography_symbols_holidays.json`)
- [x] Curation rationale documentation: captured per-fact in the
      `curation_rationale` field, in the data files themselves, as
      decisions are made — not reconstructed after the fact
- [ ] Facts 125 (Independence Day) and 126 (three national holidays)
      overlap in content (Independence Day is the lead example in both).
      Decide: keep as two standalone Facts, or merge into one structural
      cluster?
- [x] Founding Fathers core facts (85-89) curated, plus the cross-category
      facts their entity hubs point to (78, 80, 83, 84, 90) — see
      `data/facts_founding_fathers.json` and
      `data/facts_colonial_and_1800s_entity_linked.json`
- [ ] Founding Fathers entity clusters are drafted
      (`data/entity_clusters_founding_fathers.json`) but not yet reviewed
      against the actual visual assets — confirm hub-and-spoke treatment
      works once real art exists, especially the Madison/Hamilton shared
      Federalist Papers spoke
- [ ] Optional design idea, not yet built: a parallel-label card pairing
      Washington ("Father of Our Country") and Madison ("Father of the
      Constitution") — worth doing once real art exists, skip if it
      overcomplicates layout
- [ ] No visual assets exist yet for any curated fact — everything so far
      is content architecture. Next real milestone is producing actual
      art/design for the pilot category before expanding to more content
