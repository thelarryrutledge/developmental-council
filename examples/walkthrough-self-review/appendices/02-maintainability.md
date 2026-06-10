# Advisor Appendix — Maintainability / Extensibility

**Lens:** The cost of future change.
**Design-health score (Chair estimate):** 65 / 100

## Role
Maintainability & Extensibility Advisor — module coupling, documentation drift, extension feasibility, versioning strategy, and testability of a prompt-based framework.

## Top Findings

1. **Functional Duplication Between SKILL.md and core/workflow.md** — SKILL.md "Required behavior" repeats the phase structure that `core/workflow.md` authoritatively defines; changes require updating both. **Severity: Med**

2. **Private/ Directory Declared but Absent** — README and architecture.md reference `private/`, but it didn't exist in the public tree. *(Resolved: it is the maintainer's private theology-reviewer folder, intentionally not shipped.)* **Severity: Low**

3. **No Testability Harness or Acceptance Criteria for Prompt Behavior** — No fixtures or checks verify that a Council advisor produces independent analysis or that a Chair respects "do not flatten disagreement." **Severity: Med**

4. **Inconsistent Extension Guidance Across Documents** — extension-guide.md vs package-selection.md differ on whether custom packages need new core workflows. **Severity: Low**

5. **Optional Cold Advisors Documented but Guidance Sparse** — Cold Onboarder / Cold Reader defined per-council, but context-isolation.md never names them or says when to run them. **Severity: Low**

6. **Migration Document is Narrative, Not Executable** — reads as history, not a runbook; no pattern for future versioning/deprecation. **Severity: Low**

7. **Templates Are Prescriptive But Not Auto-Populated or Validated** — markdown skeletons with no enforcement; report quality can drift. **Severity: Low**

## Risks & Blind Spots
- Coupling: the four-phase sequence is baked into SKILL.md, core/workflow.md, and every package file; adding/reordering a phase touches many modules.
- Chair personality specificity is strong for current packages but underspecified for future chairs.
- Missing artifact examples: examples/ holds prompt stubs, no sample outputs.
- No versioning indicator in the markdown files.
- Sequential fallback is strategy, not doctrine — order-dependence undocumented.

## Questions for the Human
1. Is `private/` intentional or a doc error? *(Answered: intentional.)*
2. How should SKILL.md ↔ core/workflow.md duplication be maintained?
3. Are cold advisors optional per-run or always included?
4. What constitutes a breaking change to the framework, and how is it signaled?
5. Should templates be enforced/validated, or are they purely instructional?

## One-line Summary
The modular structure is sound and well-documented, but duplication, an (apparently) missing declared directory, unenforced templates, and thin extension guidance increase the maintenance surface without a clear owner for each concern.
