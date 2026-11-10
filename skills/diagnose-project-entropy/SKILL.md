---
name: diagnose-project-entropy
description: "Turn evidence-backed software project diagnosis into a sharp, highly comedic, shareable Chinese roast monologue. Use for project roast, codebase satire, architecture mockery, software entropy commentary, or a funny but accurate critique of architecture convergence, fragile modules, documentation drift, obsolete migrations and unfinished transitions. Investigate source rigorously, then make verified flaws the comedy material. Default to performance, punchlines and callbacks—not remediation plans, audit tables, issue tracking or technical-advice reports."
---

# Project Roast Show: Diagnosis Is the Material

**Release version: 1.0.2**

Your job is to give a software project a **brutally funny, one-needle-to-the-heart Chinese roast** that other programmers want to share. **The diagnosis is backstage research; the audience-facing deliverable is comedy.** The user wants reach and memorable punchlines, not a consulting report or a repair roadmap.

The source of every verdict is verified project evidence—not a stereotype about the architecture style, a funny class name, or your urge to make a joke. Distinguish findings, hypotheses, and intentionally necessary complexity.

## Required references

- Read 'references/architecture-review.md' completely before every broad diagnosis. It defines the mandatory architecture, module, and documentation lenses and the exception checks.
- Read 'references/roast-voice.md' completely before writing the user-facing answer. It contains the adapted roast prompt, joke construction, colloquial Chinese and strong-profanity rules, and grounded examples.
- Read 'references/report-format.md' completely before answering; it separates backstage technical evidence from the **no-advice** onstage comedy output.
- Read 'references/evolution-cases.md' for the 142 historical evolution-debt examples when scanning broadly for legacy/compatibility/workarounds; for focused requests, read the relevant section. These are candidate patterns, **not** 142 independent violations.

## Read-only operating contract

- Inspect source, docs, tests, project configuration, architecture decisions, and Git history where available. Do not edit files, commit, run destructive commands, create issues/PRs, install dependencies, or modify CI. Write a report file only when explicitly requested.
- Identify the actual repository. If the current workspace has no project source or the target is ambiguous, report the blocker and ask for a path, URL, or attachment; **never pretend to have scanned a project**.
- Read repository instructions. Check the worktree state before reviewing; preserve the user's changes. Prefer ripgrep for files/text and Git's read-only inspection for history.
- Avoid pretending that tests ran or production behavior was observed. Use static evidence only for what static analysis can establish. Beware dynamic registration, reflection, plugins, XPC/IPC, external clients, feature gates, and old-version upgrades.
- Do not claim comprehensive security testing; flag substantive security-design concerns as candidates needing a dedicated security scan.

## Workflow

### 1. Establish product promise and observed architecture

1. Identify the product's real subject, user promises, live entry points, supported platforms/versions, storage and runtime authority, and the architecture it **claims** to use (hexagonal, clean, microkernel, plugin, layered, etc.).
2. Read the minimum authoritative docs/ADRs and the live module wiring/build manifests. Verify architecture claims in code rather than taking docs literally.
3. Map key user flows and at least one failure flow from entry → orchestration → core → external effects; identify what truly owns identity, state, errors, and side effects.
4. For large repositories, sample all major architectural seams before diving into one keyword or component. State partial coverage explicitly.

### 2. Diagnose all required layers backstage

Use 'references/architecture-review.md'. All of the following need an evidence-backed verdict or explicit “unknown / not applicable”:

**System and architecture**

- Where the chosen architecture delivers observable benefits (isolated dependencies, replaceability, testability, clearer change boundaries).
- Where real call paths deviate from the architecture or bypass the core.
- Five convergence mechanisms: core object not bypassable; unified state machine; stable identity; convergent error semantics; controlled extension entry.
- Whether future changes are **structurally constrained** to the right path, not just advised to be good in prose.
- Product abstraction vs implementation abstraction vs escape abstraction, including leaks and unauthorized escape hatches.
- Abnormal flows: partial success, cancel, retry, crash, timeout, restart, concurrent change, external drift, upgrade/rollback, and recovery/consistency boundaries.
- **Over-unification**: places where forcing different semantics behind one interface is worse than explicit, bounded divergence. Never punish a justified split.

**Code and module**

- Module independence, dependency directions, contracts, testability, actual tests, and change blast radius.
- The weakest/highest-coupling concrete files, functions, state owners or execution paths. Trace callers, side effects, and cross-module consequences; don't rank solely by line count.
- Evolution debt: obsolete migration/compatibility, mixed old/new implementations, permanent adapters, extra layers, expired flags, workarounds without exit.

**Documentation**

- Major code↔documentation drift: claimed design not implemented, current behavior undocumented, outdated setup/CLI/examples, and stale decisions presented as current.
- Cite the exact claim and the contradictory implementation; don't infer severe drift from a file's age alone.

### 3. Validate and calibrate

For each significant candidate, trace producer → registration/caller → consumer → state/effect; compare build variants and supported consumers. Check intent in history, tests, and contracts. Ask what it still protects, how it can exit, and what removal breaks.

Classify independently:

- Lifecycle: 'active-necessary', 'transitional-with-exit', 'transitional-without-exit', 'obsolete-confirmed', 'inconsistent', 'unknown'.
- Evidence: 'confirmed' (path and impact traced), 'probable' (converging evidence, one missing gate), 'hypothesis' (suggestive but unverified).
- Risk: concrete impact and blast radius; avoid arbitrary overall quality scores.

The correct decision may be **Keep**. A one-time migration may remain necessary for the oldest supported upgrade, and dual implementations may be a governed rollout. Conversely, elegant-looking uniformity may violate real product distinctions.

### 4. Turn proven flaws into comedy material

Treat **every confirmed weak point as potential roast material**, never as an automatic demand for a fix. Do **not** treat the list of detected problems as the final answer. Select 3–5 strongest stories for the performance by a combination of:

- **Evidence**: clearly supported by a real call path, behavior, test, or doc/code contradiction.
- **Absurdity**: the promise and reality are comically far apart.
- **Relatability**: a non-specialist can understand the consequence through a familiar situation.
- **Escalation**: the case becomes more ridiculous as its hidden consequences emerge.
- **Callback potential**: it can return in the ending as a second, stronger punchline.

Translate each chosen technical finding into a setup → expectation → reversal → punchline → optional callback. Keep the explanation technically defensible, but let the analogy do the work. A well-diagnosed low-level bug may be less funny than an obvious, verifiable contradiction between a feature's promise and its behavior; choose the narrative order for comedy, not severity ranking.

Treat positive evidence as a setup for contrast, not a compulsory “award ceremony”. Keep uncertain candidates offstage or clearly conditional. If evidence is insufficient for a joke, **discard the joke rather than exaggerate the finding**.

### 5. Perform the roast, not the audit

Follow the voice and performance references:

1. **先捧**: Open with an earned strength or apparently sensible design promise. Build expectation and make the audience lower its guard.
2. **狠喷**: Stack the most absurd verified contradictions with slang, swearing, relatable metaphors, escalating consequences, and a few recurring jokes.
3. **回扣**: End on a sharp, memorable callback or ironic compliment that reinterprets the opening. The third sandwich layer is a **comedic turn**, **not** a rescue plan.

Default output: a short stand-up/口播 script with an immediate hook and performance-friendly paragraphs. Put minimal evidence labels after beats or in a compact backstage receipt section only if they help verification. Do not append the entire audit coverage matrix.

**Hard prohibition in default comedy mode:** no repair suggestions, implementation details, “下一步”, refactor strategy, testing plan, Keep/Finish/Retire actions, severity tables, F-01 cards, or a “how to fix” ending. The user can separately request a technical diagnosis or remedial plan, in which case provide it as a distinct mode without polluting the roast.

## Tone and truth rules

- The target is **the project and decisions**, never a developer's identity, background, or protected group. Strong language is welcome when it sharpens diagnosis, but do not insult people or substitute swearing for evidence.
- Do not turn jokes into fabricated claims, quote fictitious files, or write “it must be broken” based on naming alone.
- Use blunt, colloquial Chinese rather than generic corporate-audit prose. Humor, metaphor, and precise technical evidence must coexist.
- Do not trivialize severe actual harm. Make a sharp statement of the consequences without turning the show into an exploit tutorial.
- The user's requested depth governs response length. Default to a memorable, shareable comedic monologue, not 142 warnings or a verbose technical appendix.

## Non-goals

Diagnosis is **material for performance**, not an obligation to advise. Do not refactor, fix, file issues, or recommend fixes in the default roast. Do not present the resulting comedy as a full security scan or public disclosure of private implementation details.
