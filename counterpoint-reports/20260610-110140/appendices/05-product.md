# Advisor Appendix — Product / Business

## Advisor
Product / Business Advisor

## Focus
Is the skill's differentiator (preserved disagreement) now well-sold, and does the product positioning match the actual default behavior?

## Key Findings

1. **POSITIONING CONTRADICTION — High severity** (undermines trust). README.md and SKILL.md headline with "four phases" as equal, parallel components. But core/workflow.md and SKILL.md "Required behavior" make clear Executor/Reviewer are *opt-in* and Council→Chair is the implicit default. New users model a full pipeline first, then discover most of the cost is optional. A signaling failure that inflates perceived complexity.

2. **DIFFERENTIATOR IS NOW WELL-SOLD — High strength.** README "When to use this" leads with "preserving disagreement" and contrasts vs. asking the model and vs. single-viewpoint tools (code-review, plan_review). The definition of controlled convergence is in README, SKILL.md, and workflow.md. Marked improvement — but the headline graphic still treats the four phases as symmetric, diluting the message.

3. **WORKED EXAMPLE IS POWERFUL BUT SELF-REFERENTIAL — Med strength.** The self-review is genuinely end-to-end and proves the council found and resolved real bugs. Not self-indulgent — but it *is* meta (framework reviewing itself), not a concrete domain example. A concrete domain example would be more persuasive to a newcomer.

4. **INDEPENDENCE CLAIM IS NOW HONEST — High strength.** SKILL.md "Independence requirement" distinguishes true multi-agent isolation from single-session personas, with explicit mode-stating guidance. Closes the prior DP1 tension; the claim is no longer unverifiable.

5. **TOKEN COST / VALUE PROPOSITION TENSION — Med concern.** "When to use this" warns the council is "slower and more expensive by design," but there's no quantified cost guidance and no cost-vs-alternative comparison. A user may invoke it, see the cost spike, and think they made a mistake.

## Major Concerns

1. **Headline graphic misaligns with actual default behavior.** README/SKILL lead with the symmetric four-phase diagram; the real default is Council→Chair. Reorder to lead with Council→Chair, position Executor/Reviewer as optional.

2. **No concrete domain-specific worked example.** Users deciding whether to use it need to see it applied to a real architecture decision, strategy memo, or writing revision.

3. **"Controlled convergence" is defined but still feels jargony.** A long sentence in multiple contexts; scanners may skip it. A callout/sidebar might land better.

4. **Scope table in core/workflow.md is good but buried.** It directly answers the cost/default question but a README reader never reaches it before mentally committing to "this sounds expensive."

5. **Product fit unclear for the person actually invoking it.** The skill is aimed at substantive/strategic work, but the operator is often an engineer/writer on a daily task. Messaging assumes the user is the decision-maker, narrowing the addressable base.

## Recommendations

1. **Reorder README headline and opening graphic** — lead with the actual default (Council→Chair = perspectives + synthesis), move the full four-phase diagram to a "Full pipeline" section.

2. **Add a concrete worked example for one of the two domains** (architecture decision or writing project): brief → 2–3 advisor snippets → Chair excerpt → Executor excerpt → Reviewer verdict, ~2–3 pages.

3. **Callout or sidebar for "controlled convergence"** — a visually distinct one-sentence definition, treated as a brand term.

4. **Quantify or ballpark the cost** — one line setting expectations (e.g., typical Council→Chair vs full pipeline ranges), so users self-select.

5. **Clarify intended user and invocation model** — a "Who should run this" sentence: best value when run by a reviewer/lead on substantive work, less useful for quick solo iterations.

## Must-Preserve Elements

- The Council→Chair independence-requirement language (closes DP1).
- The "When to use this vs. alternatives" framing (leads with preserved-disagreement).
- The Scope table (clearest statement of actual product behavior).
- The self-review worked example as historical proof; keep it unedited even if a concrete example is added.

## Confidence
Medium. The differentiator is now well-articulated and the independence claim honest, but the positioning contradiction still misaligns product perception with reality, and the lack of concrete domain examples limits persuasiveness.

## Notes for the Chair
Real progress on honesty and clarity. The independence language is sound and the "When to use this" framing leads with the right insight. But the headline graphics suggest four equal phases when the actual default is two (Council→Chair) with optional, speculative additions. Correcting that one ordering issue aligns marketing with reality and reduces perceived complexity. A concrete domain example would be far more persuasive than the self-review; the cost is still under-explained — a ballpark would help users self-select.
