# Advisor Appendix — Maintainability

## Advisor
Maintainability Advisor

## Focus
Single-source integrity and drift-risk after the controlled-convergence consolidation pass.

## Design-Health Score
62 — Consolidation of "controlled convergence" to one source succeeded, but the pass created three new fault lines: orphaned core modules, metadata schema documented in one place but claimed by two, and a README "How to invoke" that overlaps SKILL.md.

## Key Findings
1. **High — Unreferenced core modules create maintenance debt.** `core/context-isolation.md` and `core/package-selection.md` hold operationally important rules but are never referenced from SKILL.md, README, or workflow.md — discoverable only by listing files. Classic orphan pattern; they will diverge first.
2. **High — Run-metadata schema lives in one place but two claim authority.** workflow.md has the full schema; SKILL.md references it without detail; README omits it. A non-file-reading platform reading only SKILL.md has no schema.
3. **Med — README "How to invoke" overlaps SKILL.md "File loading" + "When to run."** Both explain triggers and package selection; neither delineates its purpose.
4. **Med — Canonical-definition-plus-echo works but adds burden.** Three copies of the one-liner must stay synchronized by hand; explicit but unenforced.
5. **Low — docs/ (architecture, extension-guide, migration) don't mention Phase 0 advisor-selection, the loop-back test, or the metadata schema** — they lag the workflow.

## Major Concerns
1. The two orphaned modules are discovery failures waiting to happen.
2. The metadata schema is a pinch point for non-file-reading platforms (SKILL.md is the entry point but lacks the schema).
3. The "canonical" claim is self-referential and unenforced; three copies can silently diverge.
4. SKILL.md's file-loading list names only workflow.md, but workflow.md depends on the two orphaned core files.
5. docs/ is diverging from the workflow after the consolidation.

## Recommendations
1. Add a "Core modules" section to SKILL.md listing context-isolation.md and package-selection.md with one-line descriptions; update File loading to mention all three.
2. Reproduce the metadata schema in SKILL.md as a fallback, with a pointer to workflow.md for the full version.
3. Consolidate invocation instructions: keep README's user-centric "When to use this"; move the technical "how" into SKILL.md and have README link it.
4. Add a sync signal next to each echoed definition ("Canonical source: core/workflow.md Phase 2. Keep in sync.").
5. Update docs/extension-guide.md and architecture.md to reference Phase 0, advisor-selection, loop-back, and metadata.

## Must-Preserve Elements
- The four-phase structure and independence rules; the modular package system; the canonical convergence definition; the "From advisors/From synthesis" ethos; the run-metadata block; the loop-back classification test.

## Confidence
High — the structure is visible and the duplication/orphan patterns are deterministic, not speculative.

## Notes for the Chair
The consolidation improved core/workflow.md but did not update entry points or secondary docs to match. The pattern should be centralize + reference + signal; only "centralize" was completed. Address orphan references, metadata hoisting, and docs sync before the next release, and record a governance rule so future additions don't repeat the pattern.
