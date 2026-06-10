# Advisor Appendix — Complexity / Overbuild

**Lens:** Complexity cost and speculative generality.
**Design-health score (Chair estimate):** 55 / 100

## Role
Complexity & Overbuilding Advisor — speculative generality, surface-area cost, and whether modular decomposition is justified by actual usage.

## Top Findings

1. **24 markdown files for two domains with near-identical structure, no active third domain** — granular modularization creates ~8× the surface area of a monolithic approach without evidence it's earning its cost. **Severity: Med**

2. **v2→v3 scope expansion (added Chair + Executor + Reviewer) without user signal that divergence-only was insufficient** — a 4× workflow expansion justified by posited future value, not documented need. **Severity: High**

3. **Context Isolation Matrix duplicates logic already in workflow.md and profile files** — a redundancy liability: changes must update three places. **Severity: Low**

4. **Package Selection occupies a full file for what could be 4–5 inline bullets** — routing rule, not reusable knowledge. **Severity: Low**

5. **Three near-identical output templates with minimal domain differentiation** — could be one parametric template. **Severity: Low**

6. **Chair and Executor files are personality profiles, not reusable logic** — stored as separate files implying reuse potential they don't have. **Severity: Med**

7. **Extension Guide promises easy domains but requires creating 5 new files (~2,000 words)** — the modular story works at design level but is expensive per domain, with no third domain planned. **Severity: Med**

8. **Migration guide exists but v2 is not in the repo** — an artifact without context. **Severity: Low**

## Risks & Blind Spots
- Premature modularization hypothesis untested: if most use cases need only Council + Chair, Executor + Reviewer are speculative.
- File-I/O assumptions embedded: modularity only pays off when the host can dynamically load files.
- No usage metrics on how often Executor/Reviewer actually run.
- Template superficiality suggests one generic template would suffice.
- Advisor profiles are not composable across councils.

## Questions for the Human
1. Has a third domain package been requested or planned?
2. What fraction of uses end at Chair vs. need Executor + Reviewer?
3. In practice, are files dynamically loaded or pasted (making the structure cosmetic)?
4. Could core/ be one file with four labeled sections?
5. Was the v2→v3 jump driven by user feedback or architectural evolution?

## One-line Summary
24 files implementing a four-phase workflow across two domains, structured for extension but with no third domain deployed and no evidence users need the Executor + Reviewer complexity beyond the core divergence–convergence loop.
