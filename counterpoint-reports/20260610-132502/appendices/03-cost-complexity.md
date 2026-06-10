# Advisor Appendix — Cost / Complexity (DP-A verification)

## Advisor
Cost / Complexity Advisor

## Verdict
PARTIALLY CLOSED — the restructure reframes the narrative hierarchy and removes symmetry in the entry points, but `core/workflow.md` still front-loaded the full pipeline before clarifying the default.

*(Chair note: the residual below was fixed in this same pass; with that edit the verdict converts to CLOSED.)*

## Evidence
- **README lines 5–14:** "At its core, the council runs two phases: Council → Chair... **This is the default**... That is the product." Hierarchical and honest. ✓
- **SKILL.md lines 12–21:** "The core of the skill is two phases... **This is the default and the product.** Two further phases are **optional add-ons**..., run only on explicit request." ✓
- **workflow.md Scope table:** correctly distinguishes Default (Council→Chair) from Full pipeline (opt-in), and explains the opt-in is by use-frequency, not architecture. ✓
- **BUT — workflow.md opening (pre-fix):** "Counterpoint v3 runs four phases" + the unadorned `Council → Chair → Executor → Reviewer` diagram appeared before the Scope section, so a reader of that file in isolation met four symmetric phases first.

## Residual or newly-introduced issues
- **Scope presentation lag in workflow.md** (now fixed): the four-phase diagram preceded the default/optional clarification. *(Resolved this pass — workflow.md now opens with the two-phase core and a separate opt-in extension block.)*
- **No new duplication:** the restructure did not introduce redundancy; each file states the hierarchy once in its own idiom.

## Confidence
High — the identity-bleed concept is resolved in README.md and SKILL.md (both lead with Council→Chair as the real product and demote Executor/Reviewer to opt-ins). The only residual was a document-ordering issue in workflow.md — a 20% remainder, not a structural misunderstanding.
