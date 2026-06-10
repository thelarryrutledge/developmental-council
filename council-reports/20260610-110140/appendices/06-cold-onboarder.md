# Advisor Appendix — Cold Onboarder

## Advisor
Cold Onboarder Advisor

## Focus
Onboarding clarity gaps, invocation ambiguity, and internal inconsistencies in the core entry points (README.md and SKILL.md only).

## Key Findings

**1. SEVERITY HIGH — Ambiguous default invocation path.** README.md claims "four phases: Council → Chair → Executor → Reviewer" as the canonical flow, but SKILL.md states "Run the Council, then the Chair (the default path)" and only runs Executor/Reviewer conditionally. A newcomer reading README assumes all four always run; reading SKILL.md, they assume Executor/Reviewer are optional. This contradicts how the tool behaves.

**2. SEVERITY HIGH — "Controlled convergence" is defined but not operationalized.** README provides a formal definition and SKILL.md repeats it, but neither explains what the Chair *actually does* with Council output. What are the mechanics? How does the Chair decide what to preserve vs. collapse? No actionable steps without reading chairs/*.md.

**3. SEVERITY MED — Missing mapping between "when to use" and package selection.** README lists "Good fits" and "Skip it for," but does not say which package to use for a writing vs engineering problem, or what to do if unsure. SKILL.md mentions packages but a cold reader must infer routing.

**4. SEVERITY MED — File loading assumption not flagged upfront.** SKILL.md says "load these files as needed" and "if the platform cannot load files dynamically, paste the relevant modules," but this conditional is buried. A newcomer on a limited platform has no early warning the skill may be partially unusable.

**5. SEVERITY MED — "Default path" does not specify inputs or outputs.** SKILL.md says "Run the Council, then the Chair (the default path)" but not: What do I pass to Council? What do I receive from Chair? Is Chair output automatically passed to Executor? How do I invoke just Council+Chair? A major "how do I actually use this?" gap.

## Major Concerns

1. **Internal documentation disconnect**: README and SKILL.md disagree on whether Executor/Reviewer are always-run or conditional.

2. **"Controlled convergence" is a marketing term without implementation scaffolding**: invoked as the selling point, but entry docs give no signal about what Chair output looks like or how to act on it.

3. **Packages are mentioned as built-in but not wired into the decision tree**: no guidance for a newcomer to choose Writing vs Engineering; the "default path" doesn't say "first select a package."

4. **Platform-specific file loading is a blocker disguised as a feature**: the skill depends on dynamic file loading, but that dependency is disclosed only mid-document.

5. **"Worked example" is mentioned but not accessible from the entry point**: README points to examples/walkthrough-self-review/ but provides no excerpt or summary in the entry docs.

## Recommendations

1. **Resolve the default-path contradiction first**: a single clear sentence stating whether the default is Council+Chair only or all four phases. Ensure SKILL.md's required behavior lists the default sequence and where user choice branches.

2. **Add a minimal "how to invoke" section to both files**: a concrete example input and output for a Council+Chair run.

3. **Create a package-selection decision tree at the top of SKILL.md**: a short table — writing/editing → Writing; architecture/infra/code → Engineering; otherwise → generic.

4. **Flag file-loading as a hard platform requirement**, moved up near "Core operating rule," with an early-failure warning.

5. **Add a one-paragraph "real run" summary to README** extracted from the worked example, so the flow is tangible without breaking the read-only entry constraint.

## Must-Preserve Elements

- The four-phase architecture and its rationale as genuinely independent phases.
- "Controlled convergence" as the core value proposition and formal definition.
- The distinction from single-viewpoint review tools (code-review, plan_review).
- Writing and Engineering as built-in packages with named components.
- The human-authority closing.

## Confidence
High. The README (four always-run phases) vs SKILL.md (Council+Chair default, Executor/Reviewer conditional) contradiction is textually explicit, and the "how do I actually call this?" and "what does Chair output look like?" gaps are reproducible from the entry points alone.

## Notes for the Chair
The skill is conceptually clean and well-motivated, but the entry documents leak implementation details (file loading, packages as modules) without connecting them to user intent. A newcomer needs to know: When should I run this? What do I type in? What do I get back? What do I do with it? The biggest win is resolving the four-phase contradiction and adding a concrete invocation example. The secondary win is moving file-loading concerns out of the critical path for a cold reader.
