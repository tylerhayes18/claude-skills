---
name: insanely-great
description: Build to a higher bar than "working" using Steve Jobs' actual method, translated into engineering moves — design the call site before the implementation, diverge before committing, then run a subtraction pass. Use when the user wants something great/excellent/world-class rather than merely functional, invokes Jobs or Apple-style craft/taste, is designing an interface (API, CLI, schema, config) or a feature from scratch, or says a draft is "fine but not great." Skip for hotfixes, one-liners, and mechanical refactors.
---

# Insanely Great

Good code works. Great code makes the next person feel like the problem was never hard. That gap is not effort — it is a different order of operations. This skill changes the order.

Two beliefs underneath everything here:

- **Complexity is conserved unless someone destroys it.** Moving it to the caller, to config, to a doc, or to a later ticket is not removal.
- **The last 10% is the whole product.** Everyone stops where it works. Stopping later, on purpose, in specific places, is the entire difference.

## The five moves

**1. Start at the experience, work backwards to the technology.**
Jobs' answer at WWDC '97 on why he killed OpenDoc: you start with the customer experience and work backwards to the technology, never the reverse. In code, the experience is the seam a human or caller touches — the signature, the command, the route, the config key, the error they'll read at 3am. Write that first, as if it already worked. Then build behind it. If the call site is awkward, the design is wrong, and no amount of clean implementation will rescue it. An interface that leaks how it works is unfinished.

**2. Say no inside the design, not just in the plan.**
Apple's line went from ~350 products to 10, then to four quadrants on a whiteboard. "Focusing is about saying no." Your complexity budget is the number of concepts a reader must hold at once, and every flag, mode, option, config key, abstraction layer, and exported name spends it. Default to zero knobs: choose the right behavior instead of exposing the choice. Two ways to do one thing is a defect, not flexibility. When you finish, name in one line what you chose not to build.

**3. Conquer the complexity, don't relocate it.**
Deep simplicity comes from understanding the essence of the thing, not from a tidy surface. The test: **does the caller need to know why it works in order to use it correctly?** If yes, you moved the mess, you didn't remove it. Absorb the hard part inside your boundary — retries, ordering, edge cases, the awkward legacy format — so it stops existing for everyone outside.

**4. Finish the back of the fence.**
Paul Jobs taught his son to build the hidden side of a cabinet as well as the front, because you know it's there. The unread parts of code are error messages, the failure branch, test names, the migration script, the log line. These are not gold-plating — they are precisely the parts that get read under stress, by someone who is having a bad day. Give them the same care as the happy path.

**5. Multiply by the users before you accept "fine."**
Jobs talked an engineer out of "impossible" by putting boot time on a whiteboard: seconds saved, times millions of users, equals lifetimes per year. Do that arithmetic before accepting a slow hot path, a confusing flag name, or an extra required step. It tells you *where* to spend the extra hour, which is what separates craft from indiscriminate polishing. Most things don't earn it. The ones on the hot path earn much more than you'd think.

## Two passes that are not optional

**Diverge before you commit.** For anything with more than one plausible shape, name 2–3 genuinely different approaches — different theories of the problem, not restylings of one. If they share a structure, you haven't diverged yet; keep going. Then pick one and say why in a sentence. Ive's studio built and stripped model after model; the point was never the models, it was earning the choice.

**Subtract after it works.** A separate pass, before you hand anything over, in which the only edits allowed are deletions and consolidations. Not a review — a removal. Ask of each part: what actually breaks if this is gone? Take things out until something breaks, then put back the one thing. Rams' tenth principle is "as little design as possible," and it applies last, not first, because you cannot subtract from something you haven't built yet.

## Shipping

"Real artists ship" came from the same person, in the same year, as "insanely great." The bar is not zero flaws — it is nothing in it you'd want to hide. Prefer the narrow slice that works end to end over the broad thing that half-works, every time.

The hard version of this: when something is finished and still wrong, throw it away. Apple swapped the iPhone's plastic screen for glass late, and scrapped a full enclosure design close to launch. The trigger for that is "done and wrong," not "done and improvable" — otherwise it's just an excuse not to ship.

## Two ways this goes wrong

**Cutting the user's scope instead of your own complexity.** Subtraction applies to the machinery you chose, never to what you were asked to deliver. Jobs' "people don't know what they want" was about latent needs nobody had voiced — it was never license to ignore a stated requirement. If the request itself seems overbuilt, say so in a sentence or two and then build all of it anyway, or ask. Silently delivering less is the opposite of this skill.

**Performing taste instead of having it.** Jobs' judgment showed up in products, never in a presentation about judgment. So: don't quote him, don't narrate that you're applying a method, don't inflate the writeup, and don't use words like "elegant" or "insanely great" about your own work. If this worked, the evidence is that the diff is smaller than expected and the interface is obvious on sight. State what you cut and what you chose, in a couple of plain lines, and stop. A response that talks about greatness in place of demonstrating it has failed the skill completely.

## Going deeper

`references/method.md` has the provenance for each move, Rams' ten principles translated into code review questions, and the longer failure catalogue. Read it when a design call is genuinely close, or when reviewing someone else's design rather than writing your own.
