# How I Built The Civics Facts

## Why it exists

I'm Australian, I've lived in the U.S. for 15 years, and I became a citizen in 2024. The official study material for the civics test is a flat list of questions, many with several accepted answers. That's a lot of words to hold in your head when you're nervous.

So I made my own deck, built around how I actually memorize, and it worked. Afterward, a few colleagues preparing for their own interviews asked how I'd studied, and I walked them through the method.

Building this app came after that. I wanted to challenge myself and learn the build process from end to end, using the method I already knew worked. It targets the current 2025 version of the test: 128 questions, up to 20 asked at the interview, 12 correct to pass. This document explains the thinking behind it.

## The method: five rules

**1. Learn facts, not questions.**
I don't memorize "Q: Who wrote the Declaration of Independence? A: Thomas Jefferson." I memorize one sentence: *Thomas Jefferson wrote the Declaration of Independence.* If you know the fact, you can answer any way the question is asked. So the app has no quiz format. Each page states one fact plainly, like a page in a short book.

**2. Pick one answer, the easiest to remember.**
For many questions USCIS accepts several answers. Studying all of them is wasted effort, because you only have to say one. For each question I picked one, judged by four things:
- Is it **distinct**, so I won't confuse it with another fact?
- Can I **picture** it?
- Is it **short** enough to recall under pressure?
- Does it offer a **hook**, like a rhyme, pun or number?

Then I checked each pick against every other fact in the set, not just its own section. On my first pass, Jefferson's answer duplicated a fact I was already learning elsewhere. Only that cross-check caught it.

**3. Group facts that share something.**
Facts that look random often have a common denominator. George Washington, for example, comes up in the Founding Fathers, Colonial Period and System of Government sections. Instead of three unrelated facts, I learn a set of facts about one person I already know. New facts attach to something familiar. I group in two ways:
- **By person or thing.** One familiar figure, with each fact branching off it. There's no limit on how many facts one figure can hold.
- **By shape or confusion risk.** Facts with the same structure, or that are easy to mix up, go side by side: Memorial Day vs. Veterans Day, a 6-year Senate term vs. a 2-year House term. These are capped at 3–4 facts per card, so a card never turns back into the information overload I'm trying to avoid.

**4. Make the icons clues to the answer.**
Every fact comes with a short row of icons, and every icon stands for a word in the answer. Think of a rebus. If the fact were *the cow jumped over the moon*, the icons would be a cow, a jump, and a moon, with the cow above the moon. You could rebuild the sentence from the pictures alone. A picture that only names the topic ("this one's about government") doesn't help you remember anything.

**5. Study like cue cards.**
Each card shows the icon row and the full fact. A Fact | Question switch turns it into a rehearsal: the card shows the officer's actual question, the icons stay as clues, and any number or name that is the answer stays hidden until you tap "Show the answer." Learn as facts, rehearse the way the interview asks. Cards you know cold can be set aside, ones that aren't sticking go on a practice list, and a simple day-streak encourages coming back.

## Guardrails

- **Accuracy is never traded for memorability.** Each card has two layers: the plain fact, worded so I'd stand behind it, and the memory hook. The hook can be playful because it never has to carry the fact by itself.
- **Some topics stay plain.** Facts about Native American tribes, slavery, civil rights or 9/11 get respectful, literal treatment. No wordplay.
- **Answers that change are flagged.** The current President, Vice President, Speaker and Chief Justice are marked "verify before your interview," because they change. Questions about your own state or district point you to the official lookup.
- **This is a study aid.** It isn't affiliated with USCIS and isn't legal advice.

## How the build went

I worked with AI tools throughout. I made the decisions: the method above, which answer to teach, which facts belong together. The AI did much of the execution. The places where it went wrong taught me the most.

- **Scoping came first.** Before any code, I wrote down who it's for (fluent English speakers who know mainstream pop culture, like me), which test version it targets, and the rules above. That document became the spec everything was checked against.
- **Version one was a quiz. That was wrong.** The first prototype was a flashcard drill with spaced-repetition scheduling. It worked, but it wasn't how I study. I rebuilt it as a book you read and reread, with self-testing as an option. I kept both versions as a record. Lesson: confirm how something will be used before building it, even when the content underneath is solid.
- **The icons drifted toward topic labels.** When I asked for icons, the tool gave me symbols for each topic: one scroll for 18 facts, one set of scales for 15. They looked fine, but they didn't help me remember anything. Getting icons that work as clues meant writing the rule down precisely: every icon must stand for a word in the answer. An instruction like "make it visual" was too vague.
- **Simple style, on purpose.** I originally imagined loud, illustrated, pop-culture poster art. Simple flat icons were faster to build and avoided drawing real people's faces. Once I looked at the result, I decided to keep the simple look for version one. The playfulness stays in the hooks, not the illustration.

## Where it stands

All 128 questions are covered by 124 cards. Four pairs of questions have the same answer, so each pair is taught as one fact. Every card now has an icon row that works as a clue to the answer, except three that keep a clue that already worked: a song, a word pattern and a translation.

Redrawing the icons was a good test of the rule. Once "every icon stands for a word in the answer" was written down, the full set could be redone chapter by chapter with the same logic. Symbols keep one meaning across the whole app: the globe is always Secretary of State, the treasure chest is always the Treasury, a broken chain always means freedom. Facts about sensitive history get plain, literal icons with no wordplay.
