# Advisor Appendix — Reliability / Failure-Modes

## Advisor
Reliability / Failure-Modes Advisor

## Focus
Identifying execution failures in the recently revised developmental-council skill: scope ambiguity, loop-back state transitions, traceability fabrication, independence self-labeling, and silent under-execution.

## Key Findings

1. **High**: **Scope default assumes but does not validate** — "If scope is ambiguous, assume Default (Council → Chair) and offer to continue" creates a single silent choice point that, if the offer is never taken, delivers only perspectives without the user's intended synthesis. An agent executing this instruction has no explicit checkpoint to confirm the user actually wanted to stop at Chair rather than implicitly continuing to Executor. The offer mechanism is advisory (a suggestion), not enforced.

2. **High**: **Loop-back rule conflates "decision objection" with "execution failure"** — The rule states "If the Reviewer's objection is really with the Chair's decision (not the execution of it), do not revise — surface it to the human." But the Reviewer template explicitly checks "alignment with Chair recommendations" and "correctness" without defining the boundary. A Reviewer can easily misclassify a correctness problem as a decision disagreement and escalate when revision was warranted, or vice versa.

3. **Med**: **Traceability attribution can be fabricated or conflated** — The Chair must "attribute each finding to the advisor lens(es) that raised it." But the template provides no structural way to enforce one-to-one traceability; an executing agent can list multiple advisors as sources for a finding that only one raised, or invent a source when synthesizing novel convergence insights the advisors did not independently surface. The Chair's own creative synthesis work (ranking, identifying patterns) cannot itself be "traced" — leaving ambiguity about what counts as "raised."

4. **Med**: **Independence self-labeling is post-hoc and unenforceable** — SKILL.md requires "Always state which mode was used." But there is no structured checkpoint at report generation time; an executing agent in single-session mode could mistakenly claim multi-agent execution, or vice versa. The requirement relies on agent honesty after the fact, not a verifiable audit trail.

5. **Low**: **Executor context isolation boundary is vague** — The context matrix shows Executor receives advisor outputs as "optional," but the rule "Stay inside the Chair's recommended path" conflicts with "Flag any missing repository context before inventing implementation details." An Executor with access to both the Chair's recommendation and the raw advisor disagreements may silently invent details to resolve a tension the Chair deliberately left unresolved.

## Major Concerns

1. **Silent phase truncation under ambiguity**: If a user's input is genuinely ambiguous about scope and the executing agent offers (but does not require confirmation of) the Executor/Reviewer continuation, the user may receive only a Chair report when they expected a full pipeline or vice versa. The default is reasonable, but the offer is optional, making under-execution silent and invisible in the final report.

2. **Reviewer escalation ambiguity will cause judgment calls that compound**: Two Reviewers reading the same deliverable may classify the same objection differently (decision vs. execution). Without a clear decision boundary, the first-pass Reviewer's judgment becomes the branch point for whether escalation or revision occurs. This is especially fragile when the Reviewer is genuinely uncertain.

3. **Traceability requirement can incentivize false precision**: A Chair pressured to attribute each finding to specific advisors may over-claim sourcing ("this came from Reliability and Operations") when the real insight is the Chair's synthesis. This makes the report appear more evidence-grounded than it is, and readers lose visibility into where the Chair's judgment ends and the advisors' independent evidence begins.

4. **Single-session independence claim cannot be verified after execution**: An agent running in single-session mode must retroactively label the mode. If the agent is uncertain whether it ran in true parallelism or sequential passes (e.g., due to platform ambiguity), it may claim multi-agent when it was persona-based, poisoning the reader's calibration of the report's actual independence.

5. **Executor can silently resolve Chair's deliberately preserved tensions**: If the Executor receives advisor outputs and the Chair's "Areas of Meaningful Disagreement," the Executor may choose an unranked tradeoff to move forward, overriding the Chair's (intentional) ambiguity. The rule "Stay inside the Chair's recommended path" is not violated — because the Executor can interpret "recommended path" as implicitly choosing the unresolved option that makes execution possible.

## Recommendations

1. **Require explicit scope confirmation at the start of Phase 1**: Before running any advisor, show the user the scope assumption, let them accept or modify it, and record their choice in the neutral brief. This makes the scope decision visible and reversible.

2. **Define the Reviewer's decision boundary with a concrete checklist**: In the Reviewer template, add a section: *"Is this an execution error or a decision disagreement?"* with explicit yes/no gates: if the artifact violates the stated recommendations or contains a technical/logical error, it is execution; if the issue is "the Chair's choice is wrong," it is decision. Document this choice in the verification report.

3. **Separate "sourced findings" from "synthesis findings" in the Chair's attribution**: Require the Chair to label each recommendation as either **"From advisors"** (list sources) or **"From synthesis"**. This preserves traceability without fabricating false sourcing for insights the advisors did not independently raise.

4. **Add an execution-time mode assertion checkpoint**: When the skill's session begins, require a statement of the execution mode based on what the host platform actually supports. Record this in the brief, not after-the-fact.

5. **Clarify Executor license by restricting unresolved-tension resolution**: Add: *"Do not resolve tensions the Chair left explicitly unresolved. If the Executor cannot produce the artifact without making an unranked choice, return to the human for a tiebreaker, do not decide autonomously."*

## Must-Preserve Elements

- The core four-phase pipeline and its purpose separation.
- The independence rule during Council (advisors do not see each other).
- The Chair's responsibility for controlled convergence and explicit preservation of unresolved tensions.
- The bounded Reviewer loop-back rule (one revision cycle, then escalate).
- The advisor report template's structure and the requirement for "Notes for the Chair."
- The "true multi-agent vs. single-session" distinction.
- Human authority.

## Confidence
High. The failure modes are structural (they arise from the rules as written) and would manifest under normal, good-faith execution. The concerns are central decision points (scope, Reviewer boundary, traceability, mode assertion) that affect every run.

## Notes for the Chair
Two tensions merit careful handling:

**Tension 1 — Traceability vs. synthesis insight**: The requirement to attribute findings to source advisors is sound for accountability, but it risks making the Chair's own pattern-finding invisible. Separating "from advisors" and "from synthesis" preserves both.

**Tension 2 — Scope assumption pragmatism vs. user intention mismatch**: The default scope is operationally sensible but is a *default*, not a *certainty*. Requiring confirmation adds a checkpoint that feels like friction but prevents silent phase truncation.
