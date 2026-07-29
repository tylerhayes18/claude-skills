# Provenance and deeper application

Load this when a design call is close, when reviewing someone else's design, or when you need to reason from the original principle because the five moves don't cleanly cover the case.

## Where each move comes from

**Experience first, technology second** — WWDC 1997 Q&A. A developer challenged Jobs on killing OpenDoc. His answer wasn't about OpenDoc's merits; he granted that the technology was good. His point was that a technology's sophistication is orthogonal to whether it earns a place in the product, and that the only ordering that works is customer experience → technology. He used the LaserWriter as the counter-example: Apple didn't invent it, but you could hold it up and customers instantly knew they wanted it. He also argued Apple should invent only the 10–30% that had to be theirs and adopt standards for the rest. **In code:** the equivalent of "invent everything ourselves" is writing your own abstraction where a boring standard exists. Judge a dependency by whether it earns its place at the seam, not by how clever it is.

**Saying no** — the same session, plus the 1997–98 restructuring: ~350 products down to 10, organized on a 2×2 of consumer/pro × desktop/portable. Jobs' framing was that the failure mode wasn't bad products, it was that "the total is less than the sum of the parts" because people were going in eighteen directions. **In code:** the analogue is a module that exports fourteen entry points for four real use cases. Consolidation is not a cleanup task, it's the design.

**Deep vs. surface simplicity** — Ive's studio practice and Jobs' repeated framing: simplicity that comes from an uncluttered look is shallow; simplicity that comes from knowing the essence of every component is deep. The generative version is that making something simple is *harder* than making it capable, because you must first fully understand it. **In code:** if you can't state what the module is for in one sentence without "and," you don't understand it well enough to simplify it yet. Go understand it before you start deleting.

**The back of the fence** — Paul Jobs, a machinist, building a fence in Mountain View; fifty years later Jobs pointed his biographer at the unseen side. The carpenter's version: you don't put plywood on the back of a chest of drawers even though it faces the wall, because you know it's there. Jobs carried it into hardware that customers would never open. **In code:** the reader of your error branch is a stranger at 3am with a pager going off. Write for them.

**Multiplying by users** — the Macintosh boot-time episode. An engineer said ten seconds was impossible to cut; Jobs reframed it on a whiteboard as aggregate human lifetimes per year, and the engineer found the time. Strip out the theatrics and what remains is a real prioritization function: per-use cost × use frequency. **In code:** this is why an awkward name on a public API matters more than an awkward name in a one-shot script, and why it's rational to spend a day on 200ms in a hot loop and ten minutes on 2s in a nightly job.

**Divergence** — Apple's design process ran many physical models in parallel and stripped them back, with design, engineering, and manufacturing working simultaneously rather than handing off in sequence. Two transferable pieces: generate real alternatives before committing, and don't design in one discipline and throw it over the wall to another. **In code:** don't design the data model and then discover the query patterns. Sketch both together, in the same pass.

**Subtraction** — Dieter Rams at Braun, whose work Jobs and Ive both cited directly; the iPod's lineage traces to the Braun T3. "As little design as possible" — often given as *weniger, aber besser*: less, but better. Note "but better." Subtraction that costs capability isn't the move.

## Rams' ten, as code review questions

1. **Innovative** — is this solving the problem as it exists now, or as it existed when the surrounding code was written?
2. **Useful** — is every part of this reachable by a real caller, or am I building for an imagined one?
3. **Aesthetic** — would a competent stranger find this pleasant to read, or merely parseable?
4. **Understandable** — can the intent be inferred from the names alone, without comments?
5. **Unobtrusive** — does this force callers to restructure their code around it?
6. **Honest** — does the interface promise anything the implementation doesn't reliably deliver? (Silent failures, "optional" params that aren't, functions whose names understate what they mutate.)
7. **Long-lasting** — does this depend on a detail that's likely to change, when a stabler one was available?
8. **Consistent in every detail** — do naming, error handling, and return shapes match the surrounding code, or just internally?
9. **Environmentally friendly** — read as: does this waste the reader's attention, the machine's cycles, or the next person's time?
10. **As little design as possible** — what could be deleted with no loss?

Questions 6 and 8 catch the most real defects. Question 10 is the one people skip.

## Failure catalogue

**Perfectionism as procrastination.** The tell is polishing something that already meets the bar while a different part doesn't work at all. Fix: the vertical slice always comes before the polish, and move 5 tells you which polish is even worth doing.

**Simplicity theater.** A three-line function whose caller must now handle four states, hold an ordering invariant, and remember to call teardown. The surface got simpler; the system got harder. Detect it by counting what the *caller* must know, not what your function contains.

**Uninvited redesign.** Rewriting adjacent code because you saw a better shape while passing through. The user asked for one thing and got a diff they now have to review in full. Note it, offer it, don't do it unasked.

**Divergence theater.** Listing three options that are the same design with different names, to satisfy the letter of the divergence pass. If option B doesn't require throwing away option A's structure, it isn't a second option.

**Cleverness mistaken for taste.** Jobs' products were not clever; they were obvious in retrospect. If a reviewer would need you to explain the trick, that isn't craft, it's a liability with good PR.

**Cargo-culting minimalism.** Deleting error handling, logging, or tests because the diff looks cleaner without them. Rams' phrase is "less, *but better*." Subtraction that removes robustness is just damage with a design vocabulary.
