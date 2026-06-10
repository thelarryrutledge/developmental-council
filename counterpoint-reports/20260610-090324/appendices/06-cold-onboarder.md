# Advisor Appendix — Cold Onboarder

**Lens:** The onboarding cliff. Receives only README.md + SKILL.md as a first-timer.
**Design-health score (Chair estimate):** 42 / 100

## Role
Cold Onboarder — never seen the project before; reads only what a newcomer encounters first (README, SKILL.md, directory structure).

## Top Findings

1. **Jargon wall with no definition: "controlled convergence"** — appears in the title, description, three filenames, and the workflow, but is never explained. It's the core value proposition and the second word in the title. **Severity: High**

2. **No worked example end-to-end in the primary docs** — examples/ holds bare prompt stubs; a newcomer never sees what the final output looks like or how long it takes. **Severity: High**

3. **"Package" is overloaded and vaguely explained** — not defined until core/package-selection.md; unclear why packages/ vs councils/ vs executors/ are separate. **Severity: High**

4. **Independence requirement is critical but buried** — a major operational constraint living in one paragraph; the precise matrix is only in docs/. **Severity: Med**

5. **"Human authority" stated but implications left to the user** — templates say "Recommended Path Forward" with no framing on whether that's a suggestion or a direction. **Severity: Med**

6. **No decision tree for when NOT to run it** — anti-patterns listed, but "is my choice low-stakes?" is subjective with no concrete rubric. **Severity: Low**

7. **"Platform compatibility" claims neutrality but setup is implicit** — no diagnostic for which execution mode (parallel subagents vs sequential) you're in. **Severity: Med**

## Risks & Blind Spots
- Missing conceptual diagram of context flow (what each stage sees vs. doesn't).
- No failure-mode / error-recovery docs (deadlocked council, insufficient Executor context).
- "Outsider-style advisor" referenced once in a table, never explained in the onboarding path.
- Templates are minimal outlines; combined with no worked example, depth/length expectations are unclear.
- Migration doc is hard to find and not linked from README.

## Questions for the Human
1. Who is the primary onboarding target (Claude Code users, vanilla-Claude pasters, agent builders, all)?
2. Is "controlled convergence" a committed term or open to a clearer name?
3. Should examples/ contain fully worked examples with real outputs?
4. Would bundling each domain's files into one package subdirectory be clearer?
5. Should there be a pre-concatenated single-file version for vanilla Claude?

## One-line Summary
The architecture is sound, but the onboarding path assumes too much: "controlled convergence" is unexplained, there's no end-to-end worked example, the package/file structure is unclear, and the independence requirement is buried — leaving a newcomer unsure how to invoke it, what to expect, or whether they need it.
