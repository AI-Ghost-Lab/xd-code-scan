# Mandatory Architecture, Module, and Documentation Review

This rubric draws on system-convergence principles. It is architecture-agnostic: evaluate the project's **own product promises and real contracts**, not whether it resembles a favored diagram. A small one-off tool may not need a microkernel or elaborate domain model.

## Contents

- Evidence rubric
- A. Architecture benefits vs deviations
- B. The five convergence mechanisms
- C. Restricting future changes to the correct direction
- D. Three types of abstraction
- E. Abnormal flows
- F. Over-unification
- G. Modules, tests, and weakest links
- H. Code ↔ documentation drift
- I. Temporal debt and retirement gates

## Evidence rubric

For each lens record: **verdict**, **what code/docs/tests show**, **runtime/change consequence**, **legitimate exception or counterevidence**, and **decision**.

Use verdicts: **benefiting**, **deviating**, **mixed**, **intentional split**, **unknown**, **not applicable**. A claim such as “good testability” must name independently testable components or tests; a claim such as “everything is tightly coupled” must trace a specific path or change diffusion.

## A. Architecture benefits vs deviations

**Architecture benefits:**

- Where external APIs, data formats, OS dependencies, UI, or persistence are genuinely isolated from product logic.
- Where ports/contracts prevent direct access to forbidden internals; where tests run without integration infrastructure; where platform replacement changes only an adapter.
- Where dependency direction, ownership and one clear public API reduce consumer knowledge.
- What became simpler *because* of the architecture? Cite examples, not slogans.

**Architecture deviations:**

- Look for UI/network/database code driving core state; adapters imported by domain; wrapper classes that expose the very implementation they purport to hide.
- Identify bypass paths, duplicate entry points, circular/implicit dependencies, direct access to low-level handles, static globals, and “special case” writes.
- Contrast the architecture's claimed boundary with an actual source→consumer chain. Document when the declared architecture is merely too ambitious for the product.

## B. The five convergence mechanisms

1. **Core product object cannot be bypassed.**
   - Identify the product's genuine subject (Document, Order, Workspace, Session, etc.). Are create/import/open/update/delete/restore routed through its authorized boundary?
   - Can clients mutate storage/runtime/external handles directly and skip invariants? Are there multiple de facto core objects?
   - Check public constructors, exposed handles, service locators, factories, bypass hooks, and feature-specific “alternative paths”.
2. **State machine is unified where semantics are shared.**
   - Find the authoritative state and legal transitions. Check partial/failed/cancelled/recovering states and transition ownership.
   - Compare booleans, status enums, persisted fields, UI state, background jobs and async callbacks. Does a second path produce impossible or conflicting states?
   - Unified does **not** mean one enormous enum for genuinely independent state axes.
3. **Identity is stable and unambiguous.**
   - Trace IDs across persisted metadata, in-memory instances, files/paths, UI selections, network or IPC messages, and migrations.
   - Is a runtime handle or mutable path mistakenly treated as stable product identity? Can two IDs point to the same entity? What happens after rename/clone/import/restore?
4. **Errors converge into coherent semantics.**
   - Identify typed failures, propagation, retryability, user-facing semantics, logging and recovery ownership.
   - Find silent catches, swallowed errors, false-success responses, incompatible error dictionaries/codes, and ad-hoc per-feature workarounds.
   - Convergence means consistent **meaning and handling**, not hiding useful distinctions behind one generic error.
5. **Extensions enter through controlled contracts.**
   - Identify sanctioned extension points, plugin registration, capability negotiation, lifecycle and failure isolation.
   - Can future features register arbitrary hidden hooks, patch core types, or directly mutate shared state?
   - Is the supposed extension boundary active in code, or only described in a diagram?

For each mechanism, explicitly mark **holds / partial / fails / unknown** with examples. When the user's requested project cannot be inspected, do not score it from memory.

## C. Restricting future changes to the correct direction

The goal is **not maximum flexibility**. Determine whether wrong additions are hard to express and right additions are easy.

- Are critical invariants enforced by types, narrow APIs, constructors, dependency rules, package visibility, module boundaries, tests, or CI checks?
- Can a contributor—or an AI coding agent—add a new feature by copying an old special case, bypassing the core, or creating an alternative state owner?
- Is there a sanctioned “one path” for adding a capability, rule, plugin, or new external source?
- Do architectural constraints survive a new module, background task, and error path? Are there negative tests that reject bypasses?
- Is the architecture too rigid for actual product uncertainty, forcing a forest of workarounds?

Avoid treating architecture docs that merely ask developers to behave as executable constraints.

## D. Three types of abstraction

| Type | Legitimate job | Warning signs | Decision question |
| --- | --- | --- | --- |
| **Product abstraction** | Express durable user-facing objects, promises, identity and lifecycle | Technical transport/framework types masquerade as product concepts; multiple semantic owners | Would this concept survive swapping the framework or storage? |
| **Implementation abstraction** | Isolate replaceable machinery such as adapter, renderer, bridge, persistence transport | Mere forwarding wrapper, excessive protocol per class, leaked concrete types, brittle mapping | What real implementation change/test boundary does this abstraction buy? |
| **Escape abstraction** | Explicitly permit a bounded exception when common semantics cannot honestly cover a capability | raw handle, unsafe config, expert mode or fallback becomes a routine bypass | Who may escape, what guarantees are lost, how is it observed/contained, and when does it retire? |

**Do not collapse these categories.** Product abstractions should constrain semantics; implementation abstractions organize replaceability; escape abstractions should reveal unavoidable exceptions rather than smuggling them into the core.

## E. Abnormal flows (the project's actual worst day)

Trace one or more **negative paths** for each relevant category; do not assume an untested scenario is broken.

| Failure/edge | Examine |
| --- | --- |
| Partial success | Metadata persisted but side effect failed; half-migrated data; transactional boundary and compensation |
| Cancellation and timeout | Interrupt at every async phase; cleanup, idempotence and visible terminal state |
| Crash/restart/disconnect | Who resumes, reconciles, rolls back, detects orphans, and avoids duplicate work |
| External drift | Path/file/process/network peer changes outside the product; stale identities and UI handles |
| Concurrent/reentrant change | Two windows/jobs/clients update same entity; state authority, ordering and locking |
| Upgrade, downgrade, rollback | Old/new schema and behavior, supported versions, feature flags and data preservation |
| Capability mismatch | Imported vs native, controlled vs observable, supported vs unsupported operations |
| Security/permission failure | Denied permissions, expired authorization, fail-closed boundaries and user recovery |

For each, determine what the system **promises**, the observed path, the invariant, the failure signal and the recovery decision. Important unavailable evidence belongs in the unknown section.

## F. Over-unification: when explicit split is healthier

Do not reward everything converging into one type/endpoint if it destroys meaningful distinctions:

- Import vs open-existing; native vs third-party; controlled vs merely observable resources.
- Durable entity identity vs ephemeral execution handle.
- Independent state axes that cannot honestly be compressed to a single status.
- Different failure/rollback or security guarantees hidden under one “common” API.

Ask whether the shared abstraction makes semantics clearer or merely forces a switch statement/fallback for every call. An **intentional split** is healthy when its boundary, allowed consumers and loss of guarantees are explicit. “One core object” does not imply one implementation or one path for every concept.

## G. Modules, tests, and weakest links

- Trace module import/dependency directions, cycles, public surface, side effects and test seams.
- Find the top 1–3 files/functions/paths with high **change diffusion**: many unrelated callers, shared mutable state, parallel implementations, branching on product modes, repeated commits across distant modules, fragile tests.
- Where available, inspect relevant Git history/changes and tests to support the estimate. Line count alone is insufficient.
- Explicitly say **what a small change there could break**, which boundaries it crosses, and what evidence would confirm the feared blast radius.
- Identify modules that actually are independent and easy to test: these are earned praise, not filler.

## H. Code ↔ documentation drift

Compare specific authoritative claims against current implementation:

1. Claimed architecture/modules/import directions vs real imports and wiring.
2. Documented API/CLI/configuration vs actual symbols/flags/defaults.
3. State diagrams, error cases, data migrations and compatibility policy vs active paths.
4. Setup/test/release procedures vs current scripts and manifest.
5. ADR/spec status (“proposed”, “planned”, “implemented”, “validated”) vs commits/tests.

Report a side-by-side **Doc claim / Code reality / Impact / Evidence** table. Classify **critical** only when the drift can mislead a production, safety or migration decision; **major** when it misleads ongoing development; **minor** when cosmetic. Also report useful documentation that matches code.

## I. Temporal debt and retirement gates

Use the 142-case catalog to find historical paths that survived their purpose. For migration, flag, adapter, rollback or compatibility candidates ask:

- What supported release/client/consumer still needs this?
- Is it live in any build, dynamic registry, CLI/IPC, or recovery path?
- Who owns it? What release, metric, invariant or explicit condition permits retirement?
- Can its deletion be demonstrated with parity tests, telemetry and a rollback plan?

Legitimate transition is **not** a code smell. A transition with no exit contract is worth calling out even if it currently works.
