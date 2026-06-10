# Advisor Appendix — Robustness / Failure-Modes

**Lens:** How the workflow fails in practice when an LLM agent executes it.
**Design-health score (Chair estimate):** 45 / 100

## Role
Robustness and failure-modes advisor evaluating single-model execution of Council → Chair → Executor → Reviewer workflows.

## Top Findings

1. **False Independence: Single-Model "Parallel" Council Advisors Cannot Actually Disagree Consistently** — When a single LLM generates all advisor reports, internal coherence collapses advisor independence; the same weights and consensus-seeking tendency apply across personas. The Chair's job of identifying "meaningful disagreement" becomes impossible. **Severity: High**

2. **Chair Fabricates Consensus When Disagreement Is Theater** — If advisor reports subtly agree (same model), the Chair either invents disagreements that don't exist or rationalizes away the lack of tension, producing a report that appears balanced while compressing real tradeoffs. **Severity: High**

3. **Context Leakage Between Phases Due to Shared Prompt/Session State** — In single-model sequential execution, working memory carries earlier advisor outputs forward even when instructed not to; the isolation boundary becomes a suggestion, not a guarantee. **Severity: High**

4. **Silent Phase Skipping: Executor and Reviewer Triggers Are Ambiguous** — "Skip if the user asked only for analysis" relies on implicit intent. "Council this architecture" could mean analysis-only or a full plan; an agent may silently skip or over-execute. **Severity: Med**

5. **Chair Cannot Separate Decision from Implementation Bias** — If the Chair is the same model that becomes the Executor, it may unconsciously prefer easy-to-implement recommendations over harder-but-correct ones. **Severity: Med**

6. **Executor "Fabricates Repository Context" Silent Fallback** — Despite the rule to flag missing context, a model under pressure to "complete" may hallucinate file paths/API contracts the human then trusts. **Severity: Med**

7. **Reviewer Cannot Catch Executor Over-Commitment to Chair Guidance** — Same-model Reviewer may be defensive rather than adversarial, over-rating its own Executor work. **Severity: Med**

8. **"Audience/Scope" Context Is Optional and Ambiguous** — Without explicit closure on who reads the report, Chair/Executor may assume the wrong reader. **Severity: Low**

9. **Determinism and Reproducibility Conflict with "Independent" Generation** — Advisor order and sampling materially change downstream reports; "re-council this" can yield radically different convergence. **Severity: Low**

10. **Final Report Assembly Assumes All Phases Ran** — "if any" clauses can leave orphaned Executor Briefs with no execution artifacts, confusing the reader. **Severity: Low**

## Risks & Blind Spots
- No explicit fallback *mechanism* for unavailable subagents/files — only a principle, with no way to verify isolation succeeded.
- "Majority opinion" bias in Chair synthesis when single-model generation smooths tensions.
- Advisor confidence scores are self-evaluated; high-confidence hallucinations get weighted heavily.
- Executor incentivized to stay inside a wrong path with no escalation route.
- No loop-back: linear workflow has no defined behavior when the Reviewer says "Needs revision."
- Copy-paste fallback for packages is a large manual step easily missed.

## Questions for the Human
1. How is advisor independence validated — separate model calls or one model in sequence?
2. What should happen if the Chair finds no meaningful disagreement?
3. When does the Executor phase *not* run?
4. If the Reviewer reports "Needs revision," what happens next?
5. How are package files loaded in practice?
6. Is there any test that advisor reports are actually independent?

## One-line Summary
The workflow's core assumption — that a single LLM can generate truly independent perspectives, identify genuine disagreement, and perform unbiased synthesis/verification — fails silently because model coherence collapses independence, context boundaries become suggestions, and phase triggers rely on ambiguous intent.
