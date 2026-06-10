# Advisor Appendix — Cold Onboarder

## Advisor
Cold Onboarder Advisor

## Focus
Are README and SKILL.md now aligned on default/phases/invocation? Can a first-time reader say what to type, what they'll get, and which package runs?

## Design-Health Score
62 — Prior fixes (defining "controlled convergence," stating the default, adding "When to use" and "How to invoke") are in place, but output-visualization gaps and soft language remain.

## Key Findings
1. **High — Residual default ambiguity in SKILL.md's "Required behavior."** README and SKILL.md now agree the default is Council→Chair, but SKILL.md's "Required behavior" section lists Executor/Reviewer inside what reads like a standard flow, so a newcomer can't immediately tell steps 4–5 are fully optional.
2. **High — "What does the Chair output look like?" is unanswered.** Both docs define controlled convergence but show zero concrete output; the only example is buried near the end of README.
3. **Med — Package auto-selection is vague.** "The skill picks by domain" — but how? Keyword? User hint? Passive voice obscures who decides.
4. **Med — "Required behavior" mixes phases with when-to-run conditions**, making opt-in phases read as mandatory.
5. **Low — Output format guidance is split.** README doesn't mention file output; SKILL.md does. A README-only reader will be surprised by file-based output.

## Major Concerns
1. "What do I type?" lacks an exact command (is there a prefix? just "council this…"?).
2. "What am I getting?" has no concrete snapshot — users can't tell if it's prose, JSON, or files with appendices.
3. "Which phases matter?" is muddied by the "Required behavior" framing.
4. No worked example clearly showing the *default* Council+Chair case (the existing one likely runs the full pipeline).
5. The independence caveat is buried; a sequential-platform user may over-trust "independent" perspectives.

## Recommendations
1. Move "what you'll get back" earlier in README, with a short output/file-structure block before the invocation example.
2. Rename SKILL.md "Required behavior" to "Default flow and optional extensions," with explicit Default vs Optional bullets.
3. Add a minimal worked example to README (first 5–10 lines of a real Chair summary).
4. Clarify package auto-selection and how to override it ("use the engineering package," "just the reliability lens").
5. Surface the independence caveat earlier (one sentence in "How to invoke").

## Must-Preserve Elements
- The Council→Chair→Executor→Reviewer visual (consistent across docs); the inline "controlled convergence" definition; the opt-in nature of Executor/Reviewer (make it explicit and early); the "When to use" guidance; the lineage acknowledgment.

## Confidence
Medium — the docs are now internally consistent on the default and phases (prior contradiction fixed), but onboarding cliffs remain: no concrete output example, buried worked-example link, soft package-selection language.

## Notes for the Chair
The default contradiction is resolved — both docs now state Council→Chair as default with Executor/Reviewer opt-in. The output-clarity gap persists but changed shape: readers can now *define* controlled convergence but can't *visualize* a Chair's output without hunting for the walkthrough. When a cold reader asks "what does this produce?", the docs should answer in under three seconds. The independence caveat is also under-weighted for sequential-only platforms.
