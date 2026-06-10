# Advisor Appendix — Reliability / Failure-Modes

## Advisor
Reliability / Failure-Modes Advisor

## Focus
Failure modes in the three new additions: the YAML metadata block, the advisor-selection mechanism, and the execution-vs-decision classification test.

## Design-Health Score
62 — The rules are conceptually sound but carry several unguarded failure modes: metadata honesty relies on post-hoc agent integrity; advisor-selection creates silent-skip paths; the execution-vs-decision test is undecidable in ambiguous cases and "escalate when unsure" becomes a persistent escape hatch.

## Key Findings
1. **High — Metadata block is aspirational, not enforceable.** "Keep it accurate" is a note to the reader, not a checkpoint. An agent can record `multi-agent` when it ran single-session, or `full-pipeline` on a truncated run; nothing verifies the block matches reality, yet it looks authoritative to downstream analysis.
2. **High — Advisor-selection creates silent-truncation paths.** "If the user names no advisors, run the full council" has no confirmation checkpoint; an agent could quietly reduce the set and record the reduction only in the internal brief, never surfacing it in the report.
3. **High — Execution-vs-decision test has no decidable boundary when "faithful execution" is ambiguous.** If the Chair left A-or-B unresolved, is the Executor choosing A "faithful execution" or "deciding the decision"? "Escalate when unsure" defaults uncertain cases to non-revision.
4. **Med — File-output-by-default creates partial-delivery failure modes.** "When file output is available" is undefined: if only markdown writes succeed, is that "files by default" or a chat fallback? Partial failure is ambiguous.
5. **Med — "Scope assumes but does not validate" remains.** Phase 0 "offer to continue" is advisory, not an enforced confirmation; the assumption lives in the internal brief, not the human-visible output.

## Major Concerns
1. Metadata honesty has no audit trail; mismatched-mode runs accumulate in output/ and poison cross-run analysis.
2. "Escalate when unsure" can become a non-terminal loop when the human is also uncertain.
3. Missing-advisor "proceed with closest, say so" can silence substitution errors.
4. Reduced-set recording is advisory; a reader of the final artifact can't tell a finding is under-sampled.
5. "From advisors / From synthesis" is stated but not mechanically required by the templates yet.

## Recommendations
1. Add an execution-mode assertion in Phase 0 (state available parallelism up front; compare at assembly; flag divergence).
2. Require visible confirmation of any scope reduction or advisor substitution, recorded in metadata.
3. Give the Reviewer a concrete yes/no checklist for execution-vs-decision before "escalate when unsure."
4. Make "From advisors / From synthesis" a mandatory template section, not guidance.
5. Define "file output available" operationally with an explicit chat-only fallback recorded in metadata.

## Must-Preserve Elements
- Four-phase separation; Council independence; Chair's preservation of unresolved tensions; bounded one-cycle loop-back; multi-agent vs single-session distinction; human final authority.

## Confidence
High — the failure modes are structural and would manifest under realistic, resource-constrained execution; the prior run independently surfaced several of them.

## Notes for the Chair
DP-B revisited: recommendations 1/2/4 add gates that make the system harder to lie about but add ceremony — a markdown skill resists checkpoints. The human must weigh observability vs. lightness. Also: "escalate when unsure" may be better reframed as "make the binary choice transparent and flag the uncertainty" — slightly more agentic, still human-authoritative.
