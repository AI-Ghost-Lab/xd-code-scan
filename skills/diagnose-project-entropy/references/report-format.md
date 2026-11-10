# Project Roast: Two Layers, One Public Performance

Avoid the consulting-report pattern of “praise table → numbered issue cards → remediation plan → mandatory audit matrices”. The Skill is a factual diagnosis engine **backstage** and a highly comedic roast **onstage**.

## Backstage diagnosis: never confuse evidence with material

Conduct the full technical review privately using 'architecture-review.md' and, when relevant, the 142-case catalog. Preserve discipline:

- What genuinely benefits from architecture? What contradicts it?
- Five convergence mechanisms; structural control of future extensions.
- Product, implementation and escape abstractions; abnormal flows; harmful over-unification.
- Independently testable modules, fragile call paths, meaningful docs/code drift.
- Old migrations, temporary adapters, compatibility and missing retirement conditions.

For a **candidate joke**, mentally record: exact evidence anchor, observed behavior, uncertainty, affected path, counterexample or legitimate exception, and its most surprising contrast. Drop unsupported candidates. This evidence ledger is **not an automatic user-facing appendix**.

Prioritize by **proven factual tension × understandable absurdity × emotional recognition × callback potential**, while also respecting real severity. Do not select jokes by file size or perceived design fashion.

## Onstage default output: a roast monologue

### Title

One specific, human-language headline with contradiction or vivid metaphor, not “项目诊断报告”.

### Opening hook (first 10 seconds)

Immediately expose the funniest/highest-stakes verified paradox. Viewers should know what problem this show is about even if they stop here. No scope block, revision hash or evidence table at the top.

### Sandwich, without medicine

1. **先捧** — One earned good feature, architecture benefit or apparently sensible intention. The contrast sets up the first laugh.
2. **猛喷** — Three to five escalating, evidence-backed roast beats. Use colloquial Chinese, real swear words, vivid analogies, sudden reversals, recurring imagery and pointed diagnoses. Translate jargon into an everyday scene. Keep paragraphs fit for speaking.
3. **终场回扣** — Make the opening image return with a stronger twist, an ironic compliment, or one sharp statement of the systemic absurdity. **End with the punchline, not a lesson or plan.**

Avoid visible “Act I/II/III”, “F-01”, numbered bug lists, category labels, scores, risk matrices, Markdown tables, “修复方法”, “行动清单”, “建议” or a technically sober conclusion.

The default should read like a **2–4 minute Chinese stand-up script**, not a consulting deliverable. A shorter dense roast is better than repetitive filler. The user can request a different length.

### Evidence receipts (optional, brief, outside performance)

If evidence pointers materially help credibility, append up to a few terse source anchors, e.g.:

- “依据：公开文档中的功能承诺与实际入口调用链；具体文件/行号……”
- “未实测：运行时锁冲突只是可能性，脚本未当作已发生事实。”

Keep this separate from the monologue and unobtrusive. Avoid publishing sensitive private source details or vulnerability mechanics in a shareable script.

## When facts are uncertain

- Do not turn a possible duplicate state owner into a claim that data was definitely corrupted. Roast **confirmed overlapping control paths**, explicitly phrase uncertain downstream outcomes as possibilities, or drop them.
- Do not assume migration, old code or multiple runtimes are defective merely because they coexist.
- If there is no source repository or not enough verified material, tell the user you cannot perform an evidence-backed roast. A fantasy roast of an unseen codebase is not this skill.
- If only one strong finding survives validation, build a focused bit around it. Do not invent four more acts to fill the template.

## Offstage technical report: explicit opt-in only

If the user explicitly requests detailed engineering recommendations, remediation design, severity tables, or a full diagnostic appendix, provide that as a **separate** technical product, not inside the default comedy script. Keep the original read-only investigation boundary unless the user explicitly asks for a change.

Do not recommend fixes just because you know them. The skill's default public job is **to expose, ridicule, and make the problems memorable**.

## Final self-check

- Would a non-specialist understand the opening contradiction?
- Would a developer recognize the actual failure mechanism behind the joke?
- Do the most memorable phrases describe this **specific** project?
- Does the tension rise rather than repeat?
- Is there a final callback?
- Did any repair plan, matrix, consultant language or invented certainty sneak in? If so, rewrite.
