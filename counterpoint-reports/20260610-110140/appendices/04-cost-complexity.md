# Advisor Appendix — Cost / Complexity

## Advisor
Cost / Complexity Advisor

## Focus
Whether v3's modular four-phase architecture with two public packages and six optional advisor profiles is earning its surface area (~22 core files, 1,000+ lines of ceremony) against actual usage value and deployment complexity.

## Key Findings

1. **High: Premature optimization toward a third domain that does not exist** — The cleanup added Scope, traceability, and loop-back guidance. The system remains structured for extensibility (five files per new domain) with only two deployed packages and zero evidence of third-domain demand. `package-selection.md`, `extension-guide.md`, and modular separation are designed for growth that has not materialized.

2. **High: Value concentration in Council→Chair unacknowledged in file structure** — Documentation states "most runs should stop at the Chair" and "Executor and Reviewer roughly double token cost." Yet the repo and entry points present the four-phase pipeline symmetrically. The architecture mirrors the default but signals parity of importance, over-suggesting ceremony.

3. **Med: Duplicated concepts across entry points** — "Controlled convergence" in SKILL.md and README.md; four-phase workflow described separately in SKILL.md (~30 lines), README.md (~25), core/workflow.md (~150). When-to-use guidance appears in four places. A change to philosophy must be updated in at least three places.

4. **Med: Speculative modularity in templates and profiles** — Three templates are near-identical in structure; advisor profiles are personality sketches with no composability across councils. Structuring them as independent files implies future reuse that does not occur.

5. **Low: Optional advisor modes (Cold Reader, Cold Onboarder) are documented but unused in practice** — Defined and acknowledged, but no guidance states when to run them or how to invoke reduced-advisor mode.

## Major Concerns

1. **Artifact-generation phases (Executor + Reviewer) carry ~40% of the system's complexity but are rarely invoked.** Two of four phases are speculative relative to real usage.

2. **File-loading assumption embedded in modularity promise.** The extension story only works if the host can dynamically load files; single-session execution makes the file separation cosmetic (copy-paste). The cleanup did not resolve this.

3. **Independence requirement in single-session execution is unverified.** The principle is documented but there are no guard rails or detection for context leakage.

4. **Migration document (v2→v3) is retained as history but may confuse future maintainers.** v2 is not in the repo; the document reads as narrative, not deprecation guidance.

5. **Cleanup *added* material (Scope, traceability, loop-back) instead of removing speculative generality.** Since the prior complexity review, the repo added material without reducing the four-phase symmetry or clarifying when Executor/Reviewer are worth the cost.

## Recommendations

1. **Reframe the primary product identity around Council→Chair with Executor/Reviewer as explicit add-ons.** Lead SKILL.md/README.md with "structured multi-perspective review and controlled convergence"; move Executor/Reviewer to a secondary "optionally..." section.

2. **Consolidate duplication: merge SKILL.md's "Required behavior" into core/workflow.md and reference it.** Keep only entry guidance in SKILL.md.

3. **Document or remove the optional advisor modes** — either add a "Lightweight mode" section with syntax, or remove Cold Reader/Cold Onboarder as documented-but-unsupported.

4. **Create a single cost/benefit decision tree** — one page answering "Council only? Council→Chair? Full pipeline?" by stakes, scope, and budget.

5. **Accept extensibility beyond two domains as speculative, or build a real third-domain example** — mark extension-guide.md as future-facing, or commit a concrete third domain as proof.

## Must-Preserve Elements

- The Council isolation rule and divergence-first philosophy.
- The Chair's controlled-convergence personality (rank, preserve tension, no false consensus).
- The Writing and Engineering packages.
- The Executor and Reviewer phases as *optional* — keep them; stop implying parity with Council→Chair.
- The worked example (walkthrough-self-review/).

## Confidence
High. The prior worked example's own Complexity advisor validated the cost/benefit mismatch. The cleanup added ceremony rather than reducing surface area. The system is working well at its core (Council→Chair) but carries speculative infrastructure for growth that has not materialized.

## Notes for the Chair
The skill is not broken. The problem is identity and narrative. The system *behaves* like a two-phase tool (divergence + convergence) with optional follow-ups, but *looks* like a symmetric four-phase pipeline. That mismatch invites users to over-run expensive phases, misunderstand the differentiator, and maintain speculative infrastructure as if it were core. The DP3 resolution honored "add no new modules" but did not aggressively remove dead weight. Treat this as a roadmap for a small consolidation pass: clarify the narrative (two phases central), fold duplication, and delay extension architecture until there is a third domain.
