---
name: spaghetti-comb
description: Review a codebase (or a diff/subtree) for the structural properties that turn code into a "bowl of spaghetti" — high coupling, low cohesion, dependency cycles, tangled control flow, hidden mutable state, and change amplification. Produces a prioritized, evidence-backed report with concrete refactors. Use when asked to comb for spaghetti, audit code structure/architecture, find tangled/coupled code, check maintainability, or "is this codebase a mess?".
---

# Spaghetti Comb

Comb a codebase for the things that make it a bowl of spaghetti, then report findings ranked by severity with specific file:line evidence and a concrete refactor for each. Language-agnostic; works in any project on this machine.

The unifying defect is **high coupling + low cohesion**: things that should be independent are fused, and things that should be together are scattered. Everything below is a measurable symptom of that.

## Scope

Default to reviewing the **whole codebase** at a structural level. If the user names a subtree, a diff, or "what I just changed," scope to that instead. Ask only if genuinely ambiguous — otherwise pick the obvious target and say what you chose.

For large repos, don't read every file. Read the dependency structure first (imports/build graph, directory layout, entry points), then drill into the worst-looking hotspots. Sample, don't boil the ocean.

## Process

1. **Map the terrain.** Identify language(s), entry points, module/package layout, and the import/dependency graph. Note the intended layering (UI → service → domain → data, or equivalent) if one exists.
2. **Run the comb** — work through the seven axes below, gathering concrete evidence (`file:line`) for each finding. Prefer tools (see Tooling) over eyeballing when available.
3. **Rank** findings by severity (see Severity).
4. **Report** using the Output Format. Every finding needs evidence and a concrete fix — never "this could be cleaner."
5. **Offer to fix** the top findings. Do not refactor without the user's go-ahead; structural changes have blast radius.

## The seven axes

### 1. Coupling (worst → best)
Push every relationship *down* this list. Flag anything in the top three.
- **Content coupling** — one module reaches into another's internals (mutating private fields, monkey-patching, depending on undocumented internal behavior). *Look for:* access to `_private`/internal members across module boundaries, reflection into other modules.
- **Common coupling** — modules sharing global mutable state. The dependency is invisible in signatures, so it's the #1 spaghetti source. *Look for:* module-level mutable globals, singletons holding state, shared config objects mutated at runtime.
- **Control coupling** — a caller passes a flag that selects the callee's internal branch (`render(x, isPreview=true, skipValidation=true)`). The abstraction leaks. *Look for:* boolean/enum "mode" parameters that fan out into `if`/`switch` inside the callee.
- Stamp/data coupling (passing whole structs for one field) is milder; note only if pervasive.

### 2. Cohesion (worst → best)
- **Coincidental** — `utils`/`helpers`/`misc` grab-bags of unrelated functions.
- **Logical** — one function doing N things switched by a type flag.
- **Temporal** — `init()`/`setup()` bundling unrelated work because it runs at the same time.
- Aim for **functional cohesion** (one module/function = one job). *Look for:* junk-drawer files, functions whose name needs "and" to describe them.

### 3. Dependency graph health
The graph (modules = nodes, imports/calls = edges) is the real object of study.
- **Cycles** are the cancer. A cycle is a strongly connected component — every node in it must be understood/built/tested together. A 20-file cycle is one 20-file module wearing a disguise. *Detect with tooling, not by hand.*
- **Layering violations** — edges pointing backward (data layer importing UI) or skipping layers (UI hitting the DB directly). Each is a future cycle.
- **God nodes** — a node with both high fan-in (many depend on it) and high fan-out (it depends on many): load-bearing *and* brittle. Dependencies should point toward stability (Stable Dependencies Principle).

### 4. Control-flow tangle
- **Deep nesting** — 4+ levels of `if`/`for`/`try`. Cognitive complexity weights nesting heavily; flatten with guard clauses / early returns / extraction.
- **High cyclomatic complexity** — branch points + 1 ≈ independent paths ≈ test cases needed for full coverage. Functions above ~10–15 are hard to test; above ~25 are effectively untestable.
- **Long functions / god methods** — 100+ lines doing many things. Loss of locality.
- **Flag-driven jumps** — state set in one place, checked far away, to simulate `goto`.

### 5. State & purity
- **Hidden inputs** — function reads global/singleton state, so its real signature is bigger than its declared one.
- **Hidden outputs** — function mutates its arguments or globals (action at a distance); effects invisible at the call site.
- **Temporal coupling** — calls that must happen in a specific order (`open(); read(); close()`) with nothing in the types enforcing it.
- Prefer pure functions and a functional-core / imperative-shell shape: shrink the surface where state mutates.

### 6. Duplication & single source of truth
- **Copy-paste duplication** — the same logic in N places; a fix means finding all N and always missing one.
- **No authoritative definition** — the same concept (a price, a user, a status) computed differently in different places. Designate one source of truth.

### 7. Consistency
- **Inconsistent conventions** — naming, error handling, async patterns, and project structure differing file to file, so every file is a fresh puzzle.
- **Leaky/ wrong abstractions** — modules that exist but hide nothing; you must know their internals to use them.

## Tooling (prefer over manual inspection)

Detect the ecosystem and reach for what's installed. Don't install anything without asking.
- **JS/TS:** `madge --circular`, `dependency-cruiser` (cycles + layer rules), `eslint` complexity rules, `ts-prune`/`knip` (dead code).
- **Python:** `pydeps`/`import-linter` (cycles + contracts), `radon cc`/`radon mi` (complexity + maintainability), `vulture` (dead code).
- **Java/Kotlin:** ArchUnit (layer tests), `jdeps`, SonarQube/PMD.
- **Go:** `go vet`, `gocyclo`, `go mod graph`, `staticcheck`.
- **Any:** language-server "find references" for fan-in/out, `git log --format= --name-only | sort | uniq -c | sort -rn` for change-coupling hotspots (files that always change together are coupled even if imports don't show it).

If no tooling is available, fall back to reading the import graph and the largest files by line count — spaghetti concentrates there.

## Severity

- **Critical** — cycles spanning many modules, global mutable state touched widely, layering inversions. These block isolated testing and make blast radius unpredictable.
- **High** — god nodes, functions with very high complexity, pervasive control coupling, duplicated business logic with no source of truth.
- **Medium** — deep nesting, long functions, junk-drawer modules, inconsistent conventions.
- **Low** — stamp coupling, localized duplication, naming nits.

Rank by *change amplification* and *unknown-unknowns* (Ousterhout): how many places a typical change touches, and how likely the code ambushes you at runtime. Those two costs are what "spaghetti" actually means in practice.

## Output Format

Lead with a one-paragraph verdict (is this spaghetti, and where is it concentrated?), then:

```
## Spaghetti Comb — <target>

**Verdict:** <1–3 sentences. Where the tangle concentrates and the single highest-leverage fix.>

### Critical
1. **<short title>** — <axis, e.g. "dependency cycle">
   Evidence: <file:line, or tool output, or the cycle path A→B→C→A>
   Why it bites: <what change amplification / test pain this causes>
   Fix: <concrete, specific refactor — break the edge here, invert this dependency, extract this module>

### High
...

### Medium / Low
<may be summarized as a list>
```

Rules:
- Every finding cites evidence. No evidence, no finding.
- Every finding has a concrete fix naming the specific edge/function/module, not "improve cohesion."
- Don't pad. If the codebase is clean on an axis, say so in one line and move on.
- Quantify where you can: cycle size, complexity number, fan-in count, number of duplicate copies.

## Anti-overreach

This skill diagnoses *structure*, not behavior. Don't flag style the linter owns, don't rewrite working code unprompted, and don't recommend a grand rewrite — spaghetti is paid down incrementally (break one cycle, invert one dependency, extract one source of truth at a time). A heroic rewrite usually just makes fresh spaghetti faster. Recommend the smallest set of changes that most reduces coupling.
