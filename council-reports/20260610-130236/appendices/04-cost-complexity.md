# Advisor Appendix — Cost / Complexity

## Advisor
Cost / Complexity Advisor

## Focus
Whether the skill is accreting procedural rules faster than it removes unused infrastructure, and whether the four-phase identity masks that Council→Chair is the real product.

## Design-Health Score
58 — Core value is solid (Council + Chair work well), but the skill shows a complexity ratchet: each review pass adds metadata, rules, and decision trees rather than pruning speculative architecture.

## Key Findings
1. **High — Complexity added each pass, not removed.** Three passes added ~74 lines of procedural rules (Scope table, advisor-selection, metadata schema, classification test, independence declaration) while retaining the symmetric four-phase presentation. The prior review recommended consolidation; this pass added ceremony.
2. **High — Entry points are redundantly authoritative.** "Controlled convergence" defined in three places; four-phase structure described in three files; scope/cost in two; when-to-use across four. A philosophy change needs 3–4 edits.
3. **High — ~50% of the architecture is speculative.** Eight profile files for two domains; package-selection.md, extension-guide.md, and the modular split are optimized for a third domain that doesn't exist.
4. **Med — Metadata/classification rules are declared but unenforced** — guidance without teeth, adding narrative complexity without operational cost control.
5. **Med — File-loading couples modularity to platform capability.** In single-session execution the file separation is cosmetic (copy-paste), and the architecture doesn't acknowledge this.

## Major Concerns
1. The self-review loop is a complexity ratchet: each pass adds procedures, none remove dead weight.
2. Executor/Reviewer are ~40% of surface area for ~5–10% of invocations, yet presented with parity to Council→Chair.
3. Information architecture treats Council→Chair as equal to Executor→Reviewer despite asymmetric cost.
4. Scope/cost guidance exists but is buried in workflow.md, not where users land first.
5. The skill is becoming self-describing (procedural prose) rather than self-implementing.

## Recommendations
1. Reframe the narrative from four-phase to two-core-plus-optional; lead with Council→Chair.
2. Merge SKILL.md "Required behavior" substance into core/workflow.md as the single source; keep SKILL.md as entry guidance.
3. Put a one-page scope/cost decision table near the top of README.
4. Mark extension-guide.md as future-facing, or commit a concrete third domain as proof.
5. Decide: keep metadata/classification as declarative guidance (don't over-specify), or build real enforcement — don't leave rules in prose without tooling or examples.

## Must-Preserve Elements
- Council isolation; the Chair's controlled-convergence behavior; the two public packages; the worked example; Executor/Reviewer as genuine opt-ins.

## Confidence
High — the v2→v3 transition was justified, but three passes later the system adds procedure without removing structural speculation; the prior complexity advisor made this explicit and it wasn't acted on.

## Notes for the Chair
The skill is not broken. The problem is identity bleed: it behaves like a two-phase product with optional follow-ups but reads like a symmetric four-phase pipeline, which invites over-running and commits ongoing maintenance to speculative infrastructure. This is a "polish the primary identity and defer the aspirational infrastructure" moment — a light consolidation, not another feature. The ratchet has turned twice; the next move should subtract, not add.
