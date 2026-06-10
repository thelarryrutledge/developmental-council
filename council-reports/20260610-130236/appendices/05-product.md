# Advisor Appendix — Product / Business

## Advisor
Product / Business Advisor

## Focus
Whether the positioning contradiction is resolved and whether invocation friction is gone for new users.

## Design-Health Score
62 — Architectural clarity is good (preserved disagreement is genuinely valuable), but repeated documentation churn without structural reconciliation keeps the same tension resurfacing.

## Key Findings
1. **High — Positioning still reads symmetric.** The README headlines four equal phases; "Council→Chair is the default" is justified mainly via a pointer to workflow.md. A cold reader doesn't see the default without following the link.
2. **High — Worked example is still only self-referential.** README points to the council reviewing itself; no concrete non-meta example of a real user problem. Second consecutive review flagging this.
3. **High — Duplication of the convergence definition.** *(Chair note: VERIFIED STALE — the README and SKILL definitions are now byte-identical; this finding reflects a prior state.)*
4. **Med — "How to invoke" is vague on which package runs.** "The skill picks by domain" gives no observable mechanism; steering ("use the engineering package") works but isn't stated as the norm.
5. **Med (strength) — Differentiator is now well-articulated.** "When to use this" strongly differentiates preserved-disagreement from asking-the-model and single-lens review. Genuinely stronger than v2.

## Major Concerns
1. The positioning has been revised three times and still reads symmetric — signal the structure may not fit the headline.
2. Cost claims are vague; precise cost is hard to state, so it should be explicitly "rough."
3. Reduced-advisor selection is advertised but mechanically unreal — declaring an unbacked feature erodes trust.
4. The independence caveat lives in SKILL.md, not README, so README readers may over-claim independence on single-session platforms.
5. Target user is never stated (individual engineer? review board? team with conflicting views?), making "When to use this" harder to internalize.

## Recommendations
1. Resolve DP-A before any further doc pass: either lead with Council→Chair (Executor/Reviewer as add-ons) or keep four-phase and redefine "default."
2. Keep a single canonical convergence definition; entry points quote/link it.
3. Create a real non-meta worked example, or stop promising one (and flesh out or remove the placeholder example prompts).
4. Make "How to invoke" operational: exact trigger, what happens next, how to steer.
5. State the target user and core use case in the opening pitch, not buried in "When to use this."

## Must-Preserve Elements
- The four-phase architecture; the preserved-disagreement differentiator; the multi-advisor independence concept; the modular package structure; the chairs' groupthink self-check.

## Confidence
High — the latest run is direct external validation, and the prior cycle's attempted fix for the same contradiction is documented to have only partly landed.

## Notes for the Chair
The contradiction was declared resolved and then kept resurfacing because the product *structure* (four equal, optional phases) may not align with the *positioning* (Council→Chair lightweight default). Until you decide the identity (DP-A), doc fixes will keep chasing the same tension. This is a choice, not a bug — make it first. *(Chair note: finding #3 here is stale; the definition wording is already unified.)*
