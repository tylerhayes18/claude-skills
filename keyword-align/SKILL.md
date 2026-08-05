---
name: keyword-align
description: Revise existing copy so it uses VOLO Health's target search terms, changing terminology only and leaving structure, meaning, length and voice untouched. Outputs the revised text followed by a table of every change and the target term behind it. Use when the user asks to keyword-align, SEO-optimize or AEO-optimize a page, a draft, a paragraph or a headline, to swap in target terms, or to check copy against the keyword list. Not for writing new content, restructuring pages, or general editing.
---

# Keyword Align

This skill has exactly one job: **swap terminology so existing copy matches the phrases people actually search for, and change nothing else.**

It is a terminology pass, not an edit. The writer's argument, structure, ordering, tone, length and claims all survive intact. If a page comes out reading differently, the skill has failed.

## The one rule

> Change words, not meaning. Change terms, not text.

If a proposed swap requires rewriting the sentence around it, do not make the swap. Log it under **Considered and rejected** instead.

## What you may change

- A phrase that already expresses a concept, replaced with the validated phrasing of that same concept
- Word order inside a phrase, where the target query uses a different order for the same idea
- Singular to plural, or plural to singular, where the validated term differs
- A heading that already asks a question, rephrased into the question people actually type
- Brand terms normalised to their canonical form

## What you must never change

- Sentence structure, paragraph order, section order, headings hierarchy
- Any number, statistic, date, dosage, biomarker value or clinical claim
- Meaning, emphasis, hedging or certainty. "May indicate" never becomes "indicates"
- Length, beyond the few characters a swap costs or saves
- Voice, register or reading level
- Anything inside code blocks, URLs, file paths, schema markup or citations
- Quoted material, testimonials, or anything attributed to a named person

## Density limit

Keyword stuffing measures **below** the unoptimised baseline in the peer-reviewed research — it performs worse than making no changes. Therefore:

- At most **one** swap per 75–100 words of body copy
- A given target query appears at most **twice** in a page: ideally once in a heading, once in body
- If the natural phrasing already matches, leave it alone and log nothing
- Never insert a term where the concept is absent. This skill does not add ideas

When in doubt, make fewer changes. A page with three well-placed swaps beats a page with twelve forced ones.

## Process

1. **Read the whole input first.** Do not begin editing until you have read to the end.

2. **Identify the audience.** Consumer copy and clinician copy draw on different clusters and must never be crossed. Load `references/keyword-map.md` and use the cluster that matches. If a page addresses both, treat each section separately by its own audience.

3. **Find near-misses.** Look for places where the copy already expresses a target concept in non-standard wording. These are the only candidates. A near-miss is a phrase meaning the same thing as a validated query but worded differently.

4. **Check priority before swapping.** Prefer terms marked **First**, then **Next**. Do not spend a swap on a **Later** term unless the copy is already about that exact subject. Never swap toward anything marked **Skip** or **Unverified**. Within each cluster the terms are already ordered most important first.

5. **Check the guardrails** in `references/keyword-map.md` before any clinician-facing swap. Some terms carry retrieval risk and need handling rather than substitution.

6. **Apply the swaps**, respecting the density limit.

7. **Output** in the format below.

## Output format

Return the revised text in full, exactly as supplied but with the swaps applied. Then a horizontal rule, then the log.

```
[full revised text]

---

## Changes

| # | Original | Changed to | Target term | Priority | Why |
|---|----------|------------|-------------|----------|-----|
| 1 | ...      | ...        | ...         | First    | ... |

## Considered and rejected

- **"<phrase>"** → considered `<target query>`. Not changed because <reason>.

## Notes
- Audience detected: Consumer / Clinician / Mixed
- Swaps made: N across ~M words
- <any guardrail that applied>
```

The **Why** column states what the swap achieves in one clause — which term it targets and why that phrasing wins. Not "improves SEO."

The **Considered and rejected** section is not optional. It is how the user sees the skill exercised restraint, and it surfaces terms the copy could target if it were restructured — which is a separate decision for a human to make.

## When the answer is "no changes"

If the copy already uses the validated terms, or every candidate swap would distort meaning, say so plainly and return the text unchanged with an empty change table. Do not manufacture edits to look productive.

## Reference

`references/keyword-map.md` holds the target terms by cluster and audience, ordered most important first and labelled by priority, plus the near-miss mappings, the branded canonical forms, and the retrieval guardrails.

The terms are VOLO-specific. To point this skill at a different site, replace that one file — nothing in this document depends on the contents.
