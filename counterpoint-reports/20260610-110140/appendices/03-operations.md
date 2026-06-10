# Advisor Appendix — Operations

## Advisor
Operations Advisor

## Focus
Operability of recent v3 architecture changes (Scope steering, reduced-advisor syntax, symlink install, observability, and graceful degradation).

## Key Findings

1. **Scope declaration exists in docs but has no self-consistent syntax or example (High).** The workflow names three scopes and mentions "reduced advisor set" with an example phrase, but no template shows how a user actually requests this, no error-case handling is documented, and no report metadata guarantees which scope was used post-run.

2. **Token cost steering doesn't measurably reduce cost; Executor+Reviewer remain undercosted relative to the Council phase (High).** The council itself (7 advisors engineering, 6 writing) costs far more than the later phases. There is no evidence that limiting to Council→Chair reduces per-run cost enough to make the "lightweight" default meaningful when most tokens are spent on advisor generation. The cost tradeoff promised in one line never appears in SKILL.md.

3. **Symlink install setup will leak output/ and private/ to ~/.claude/skills/, creating discovery confusion and potential privacy/credential exposure (Med).** Installing as a symlink to the repo exposes run artifacts (gitignored) and any private profiles/secrets. Install docs say "use this directory as the skill folder" with no symlink guidance.

4. **No structured observability: post-run, there is no machine-readable way to know which scope/mode/advisor-count/independence-model was used (Med).** The report header is unstructured prose. No frontmatter fields, no JSON metadata, nothing for cost attribution, SLA measurement, or debugging independence failures.

5. **Reduced-advisor syntax is recommended but not defined as a mechanic (Med).** Docs say "honor an explicit request for a reduced set" but do not specify whether this is a natural-language heuristic, a tagged parameter, or a brief field. No Chair behavior is defined for "user asked for 3 but I only have 2 available."

## Major Concerns

1. **Default scope steering is not observable to the executor.** The executing model has no explicit signal of which scope was requested; ambiguous briefs default to Council→Chair but the executor does not know it could have continued. The opposite also occurs: "run the full council" has no validation it actually ran, or ran only once.

2. **True multi-agent independence is asymmetric with documentation.** SKILL.md says "always state which mode was used," but workflow.md and the example report don't show *how* to determine it or what the human should do in degraded mode.

3. **Symlink + gitignore interaction will surprise a maintainer.** output/ is gitignored in the repo but exposed via the symlink; a maintainer seeing a clean `git status` won't realize output/ is accumulating artifacts.

4. **Cost tradeoff claim is vague and unvalidated.** "Executor and Reviewer roughly double the work" may be wrong — if most tokens go to the council, adding Chair/Executor/Reviewer is ~30% more, not a doubling.

5. **No graceful degradation path for platforms without subagent or file-output support.** README mentions fallbacks but no phase-by-phase fallback is documented, and no test harness validates the sequential fallback.

## Recommendations

1. **Make scope/mode/advisor-count metadata explicit and structured** — a YAML frontmatter block at the top of every report (scope, advisor_count, execution_mode, estimated_token_cost, run_timestamp, reduction_reason), or a sidecar `.metadata.json`.

2. **Define the reduced-advisor syntax as a formal parameter or inclusion list in the brief**, with an example in the templates and a defined behavior for missing/named advisors.

3. **Clarify symlink install behavior** — document the symlink pattern, note output/ and private/ exposure, and recommend `output/.gitkeep`.

4. **Validate the cost claim with a real baseline or remove it** — capture token costs per phase and publish concrete numbers, or replace "roughly double" with "costs vary by scope," plus a one-line upfront cost note in SKILL.md.

5. **Document the sequential-fallback behavior as a labeled execution mode**, not a transparent fallback, with explicit report-header labeling and a groupthink check on near-total convergence.

## Must-Preserve Elements

- The three-scope model (Default, Full pipeline, Review only).
- The bounded loop-back rule.
- The groupthink check in Chair profiles.
- The modular file structure.
- The independence requirement section in SKILL.md.
- The symlink install pattern itself (just needs clarity).

## Confidence
High. The recent changes are correct in principle. The weaknesses are observability and operational mechanics — structured metadata, syntax definition, cost validation, transparency about fallback modes. None require architectural rework.

## Notes for the Chair
The system is not broken, but it is under-instrumented. Scope steering is declared but not syntactically usable without tribal knowledge. The cost tradeoff is claimed but not validated. The independence model is honest in SKILL.md but operationally vague: no maintainer can tell post-run whether they got true isolation or degraded personas. The symlink install will confuse a future operator unless documented. Fix metadata, syntax, cost baseline, and install clarity and the skill becomes operationally boring and trustworthy.
