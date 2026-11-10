# Evolution-Debt Pattern Catalog (142 cases)

This is a normalized catalog of software evolution-debt patterns, designed as prompts for investigation rather than a certified inventory of defects. Use the list for **recall**, not as 142 rules to blindly enforce. A match is only a candidate until code paths, supported contracts, usage, and history validate it.

## Contents

- Cases 1–22: Time-limited decisions
- Cases 23–52: Complexity, state and abstractions
- Cases 53–72: Data, authority and lifecycle
- Cases 73–92: Debug, tests and dependencies
- Cases 93–112: Dead code and recovery
- Cases 113–142: Boundaries and deletion governance
- Evidence-first interpretation

## 1–22: Time-limited decisions that outlived their purpose

1. Temporary workaround becomes permanent.
2. One-off version migration survives long after its only intended transition (e.g. v1.0 → v1.1).
3. Feature flag is never retired.
4. A/B experiment remains after the decision.
5. Compatibility for unsupported old clients remains indefinitely.
6. Customer-specific compatibility persists after the customer/use case disappears.
7. Incident-PTSD defensive branch survives without current evidence.
8. Guard against a long-fixed bug becomes permanent.
9. Architecture migration stops halfway, leaving old, new, and bridge pipelines live.
10. Adapter intended as a transitional bridge becomes a core dependency.
11. Deprecated API or implementation is never removed.
12. Old and new names for one concept coexist after incomplete rename.
13. Duplicate utility functions evolve independently.
14. Copy/paste implementations diverge into parallel variants.
15. “Wrap it once, refactor later” creates another permanent indirection.
16. Temporary configuration becomes public/stable protocol.
17. Test-only code invades production architecture.
18. Mock constraints begin dictating production design.
19. Exception paths become much more complicated than normal paths.
20. “Just in case” checks accumulate without an explicit threat/failure model.
21. Enum contains retired historical states.
22. Many booleans collectively encode an undocumented implicit state machine.

**High-value transition probe:** Compare an old input → legacy processor, a new input → replacement pipeline, and the compatibility adapter bridging them. Who has write authority? Is there a target cutover version, owner, parity test, and a deletion event? Three simultaneous paths are not automatically a bug during rollout.

## 23–52: Complexity, state, abstractions, and configuration

23. Cache layered over another cache.
24. Synchronous and asynchronous implementations both remain live.
25. Callback, Promise, and async/await generations coexist without clear contract.
26. Old database schema is carried indefinitely.
27. Data model only adds fields and never removes obsolete semantics.
28. Optional/nullable types proliferate to hide unclear invariants.
29. God Object grows gradually.
30. Manager wraps another Manager without real responsibility separation.
31. Singleton dependencies spread globally.
32. Global mutable variables become implicit APIs.
33. EventBus creates an invisible invocation chain.
34. String-based notification names act as magic APIs.
35. Middleware layers accumulate.
36. Hooks accrete without a clear owner or removal strategy.
37. Special-case subclasses make inheritance trees unwieldy.
38. Legacy abstract base class has no real implementation/use case.
39. Protocol/interface exists only for hypothetical future needs.
40. Over-generalized infrastructure obscures the current business problem.
41. “Might need later” code is retained without users.
42. Old log formats remain active.
43. Error code conventions from multiple generations are mixed.
44. Errors are silently swallowed.
45. Retry logic masks an underlying failure.
46. Timeout values persist without a rationale.
47. Magic numbers become de facto compatibility protocol.
48. Configuration file becomes its own programming language.
49. Configuration combinations produce uncontrolled state space.
50. Environment variables accumulate as implicit compatibility switches.
51. Old CLI parameters remain supported without documented clients.
52. Old file paths remain compatible indefinitely.

**Probe:** Look beyond text matches. A tiny legacy interface may have more change diffusion than a huge but isolated module. Distinguish a necessary compatibility contract from indecision.

## 53–72: Data migrations, sources of truth, and resource lifecycle

53. File format compatibility layers pile up.
54. Serialization fields can never be repurposed because historical consumers are unknown.
55. Database migration chain grows without a lifecycle policy.
56. Migration needs a migration of its own.
57. Patch fixes another patch.
58. One concept has multiple sources of truth.
59. Synchronizing states introduces additional synchronizing state.
60. Nobody owns stopping a background job.
61. Observer/listener is registered but never deregistered.
62. Resource lifecycle has no explicit owner.
63. Lock is added as a local thread-safety patch without a coherent concurrency model.
64. Deadlock is “solved” by a timeout.
65. All work is serialized to avoid solving concurrency correctness.
66. Performance shortcut bypasses an original contract.
67. Fast path becomes the actual primary path.
68. Cache invalidation logic exceeds business logic.
69. Precomputed results drift and become untrustworthy.
70. Reconciliation logic itself needs another reconciliation loop.
71. Watchdog needs another watchdog.
72. Health check becomes an unexpected business dependency.

**Probe:** Trace authority, invalidation, task cancellation, shutdown, retries, and recovery. Do not declare concurrency bugs from naming alone.

## 73–92: Debug, tests, dependencies, and names

73. Debug capability reaches production.
74. Hidden debug menu persists.
75. Temporary script becomes critical infrastructure.
76. Nobody dares modify a legacy Bash script.
77. CI workaround becomes permanent.
78. Tests are altered merely to make a red build green.
79. Golden files grow beyond anyone's understanding.
80. Tests preserve historical behavior rather than intended behavior.
81. A bug becomes an external compatibility guarantee.
82. Consumers rely on undefined behavior.
83. Dependency upgrade failure causes a permanent fork.
84. Vendor patch survives indefinitely.
85. Entire obsolete dependency is retained for a single helper.
86. Dependency upgrade adds an indefinite compatibility wrapper.
87. Internal API accidentally becomes public API.
88. Directory structure reflects organizational history rather than current responsibility.
89. File names no longer describe current meaning.
90. Class names accumulate V2/V3/V4 generations.
91. TODO comments become permanent documentation.
92. FIXME comments no longer identify a concrete problem.

**Probe:** Verify actual production exposure, reproducibility, dependency ownership, public consumers, and supported test contracts before judging.

## 93–112: Dead code, recovery branches, and policy erosion

93. Comments describe an obsolete implementation.
94. Commented-out old implementations are never removed.
95. Apparently dead code is preserved because dynamic reachability is uncertain.
96. Legacy directory becomes a permanent dumping ground.
97. Experimental directory is promoted to production by accident.
98. Temporary-named class survives for years.
99. Compatibility layer starts adapting another compatibility layer.
100. Refactoring adds a replacement but never removes the old path.
101. Failed new system causes old system to be revived without retiring either.
102. Rollback path remains permanently active after cutover.
103. Canary implementation becomes normal implementation without consolidation.
104. Version checks multiply.
105. Platform differences duplicate entire modules.
106. Regional special cases spread.
107. Old authorization checks remain after a permission-model migration.
108. Security patch becomes a permanent bypass or special exception.
109. Blacklist expands without expiry/review.
110. Whitelist expands without expiry/review.
111. Rule priority is repeatedly patched.
112. Special cases overtake the general rule.

**Probe:** Some recovery and rollback code is necessarily long-lived. Distinguish dormant *capability* from obsolete *production path*. For security-related claims, require concrete authorization/data-flow evidence.

## 113–142: Boundary erosion and missing deletion governance

113. Business rules are duplicated across UI, persistence, and network layers.
114. Validation is repeated with inconsistent allowed ranges.
115. Permission checks differ by endpoint or subsystem.
116. ORM/database schema starts defining the domain model.
117. Network DTO is used directly as a domain object.
118. UI state becomes authoritative business state.
119. Presentation logic leaks into the core.
120. A briefly fashionable programming paradigm leaves residual code.
121. Framework trends leave multiple architectural strata.
122. Each developer's personal style becomes a separate mini-system.
123. Former employee's code remains untouchable.
124. “It is stable” becomes the sole argument against necessary refactoring.
125. Original user requirement no longer exists, but implementation remains.
126. Removing UI does not remove the associated feature/path.
127. Hidden feature intended for later deletion is never deleted.
128. Lack of monitoring prevents anyone from proving deletion safety.
129. Code without an owner lives indefinitely.
130. Temporary code lacks an explicit expiry condition.
131. Closing an issue means implementation is done, not that feature lifecycle is done.
132. Releases have add gates but no remove gates.
133. Review asks whether code works, never when it should disappear.
134. Technical debt is recorded, but no repayment trigger is scheduled.
135. “Refactor later” becomes psychological reassurance.
136. Hard-to-delete code is kept, making future deletion even harder.
137. Historical behavior becomes an unquestioned default.
138. Strange code is mistaken for hidden institutional knowledge.
139. Fear without evidence prevents cleanup.
140. Source repository becomes an accidental database of product history.
141. A ten-year-old product runs ten years of accumulated historical behavior.
142. The final problem is not simply too much code, but not knowing what can be **safely deleted**.

## Evidence-first interpretation

Every candidate must answer these questions before it becomes a finding:

1. **Is it live?** List actual entry points, dynamic registrations, supported builds, and consumers.
2. **Why is it here?** Find the historical decision/incident/release or clearly mark unknown.
3. **What does it protect?** Supported upgrade, data preservation, SLA, public API, rollback, compatibility, tests, or nothing demonstrated?
4. **What is the exit contract?** Owner, end condition, cutover gates, monitoring, tests, and removal deadline/event.
5. **What changes if it goes?** Behavior, persistence, security, performance, operational recoverability, and rollback risk.

The outcome may be **Keep**. A clean report recognizes intentionally necessary complexity, not just removable code.
