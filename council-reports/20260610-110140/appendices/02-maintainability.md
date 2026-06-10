# Advisor Appendix — Maintainability

## Advisor
Maintainability Advisor

## Focus
Duplication of authoritative content between SKILL.md/README.md and core/workflow.md; inconsistent terminology; divergent "When to use" guidance across entry points.

## Key Findings

1. **CRITICAL — Dual definition of "controlled convergence"** (High)
   - SKILL.md line 10: "never collapsing disagreement"
   - README.md line 18: "rather than collapsing disagreement"
   - Semantic drift — README is prescriptive, SKILL is absolute. Neither refers to workflow.md where this should be the single source.
   - Risk: new maintainers may sync only one file and create divergence.

2. **Divergent "When to use" guidance across entry points** (High)
   - SKILL.md "When to run": trigger phrases, then do/don't lists (operational framing)
   - README.md "When to use this": comparative positioning (why vs alternatives), then fits/skip (strategic framing)
   - Users reading SKILL.md miss the "vs code-review" and "vs asking directly" reasoning. Readers of README miss explicit trigger phrases.
   - These are not complementary — they're alternative mental models with no cross-reference.

3. **Traceability requirement split across Phase 2 and template** (Med)
   - workflow.md line 78 and convergence-report.md line 21 phrase the same requirement differently. If one is updated, the other risks divergence. advisor-report.md template does not mention this at all.

4. **Missing scope guidance in README.md** (Med)
   - core/workflow.md has authoritative "Scope" section: default is Council→Chair, full pipeline is opt-in, cost implications stated.
   - README.md has no equivalent section. Users reading README may not understand that Executor/Reviewer are not default.

5. **Advisor-report template does not specify traceability need** (Low)
   - convergence-report template requires "source advisors" per finding; advisor-report template has no parallel requirement, so advisors may not know they need to be traceable.

## Major Concerns

1. **Single-source-of-truth breaking for "controlled convergence"**: Three mental models now exist — the abstract definition (SKILL/README), the Phase 2 operational requirement (workflow.md), and the template requirement (convergence-report.md).

2. **No cross-reference between entry points**: SKILL.md defers to core/workflow.md as authoritative, but README.md does not. README stands alone, creating two parallel authoritative sources.

3. **Scope/default-path guidance is scattered**: SKILL.md says "default path," workflow.md explains it in a table, README never mentions it.

4. **Terminology drift in advisor output vs. chair output**: "Key Findings" means different things in advisor-report (lens-specific) vs convergence-report (reconciled). Not documented.

5. **docs/ may not reflect recent changes**: architecture.md, extension-guide.md, migration-v2-to-v3.md do not mention the Scope section, traceability, or the bounded loop-back rule.

## Recommendations

1. **Consolidate "controlled convergence" to a single canonical definition** in core/workflow.md; have SKILL.md and README.md link to it with a one-line inline summary.

2. **Add cross-references between SKILL.md, README.md, and workflow.md**; have README's "When to use this" defer to SKILL's trigger phrases and link to the Scope section.

3. **Make Scope guidance non-optional**: add a "Scope and cost" reference to SKILL.md mirroring workflow.md's table (do not repeat — reference it).

4. **Require traceability annotation in advisor-report template** so advisors surface which lens raised each finding.

5. **Audit docs/ against recent changes**; add "Last updated / reflects core workflow version" notes.

## Must-Preserve Elements

- The Council-independence vs later-phase-access distinction.
- The bounded Reviewer loop-back rule.
- The separation of advisor lenses, consolidated as traceable inputs to the Chair.
- The package structure (councils/chairs/executors/reviewers as composable units).
- Human final authority.
- The definition of controlled convergence as preserving disagreement, not faking consensus.

## Confidence
High. Three files now each carry authoritative-sounding definitions of core concepts with inconsistent phrasing and missing cross-references. These will diverge under maintenance pressure unless consolidated.

## Notes for the Chair
The cleanup removed `private/` references and unified the workflow description, which was correct. But it introduced **distributed authority over core concepts**: the convergence definition, scope guidance, and traceability requirement now live in multiple places with no single source of truth. The README expansion (comparative positioning) is valuable but invisible to SKILL.md readers, and SKILL.md's trigger phrases are invisible to README readers. The tension is fragmented entry points that each feel complete but are not. Unify: one authoritative definition per concept, with entry points that defer to core/workflow.md and link to each other.
