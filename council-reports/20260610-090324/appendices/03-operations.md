# Advisor Appendix — Operations / Usability

**Lens:** Real-world operability — cost, latency, steering, observability, degradation.
**Design-health score (Chair estimate):** 50 / 100

## Role
Operations / Usability Advisor — token/time economics, user steering, observability, and graceful degradation of running the skill.

## Top Findings

1. **High token cost per invocation with unclear ROI threshold** — 6–8 advisors + Chair + Executor + Reviewer can burn 80K+ tokens before a usable artifact; no guidance toward a "lite" path. **Severity: High**

2. **Advisor independence requirement creates implementation burden for sequential execution** — no explicit recipe, reference implementation, or leakage-prevention guidance for the no-parallelism case. **Severity: High**

3. **Output volume and digestibility risk** — Exec summary + CCR + Executor + Reviewer + 7-advisor appendix easily exceeds 8–12K tokens with no enforced curation. **Severity: High**

4. **Weak affordance for steering and phase skipping** — no lightweight syntax for "Council + Chair only" or "3 advisors not 7"; the trigger surface is binary. **Severity: High**

5. **Poor observability of which phase produced what finding** — no traceability from a final recommendation back to the advisor that raised it. **Severity: Med**

6. **Graceful degradation gaps for missing tools** — assumes file output; no prescribed fallback UX when files can't be written. **Severity: Med**

7. **Onboarding friction for first-time users** — triggers, four phases, packages, councils/chairs/executors/reviewers, isolation rules, templates — a lot to absorb. **Severity: Med**

8. **Package selection is implicit, not explicit** — the skill guesses the domain with no validation step. **Severity: Low**

## Risks & Blind Spots
- Latency surprise: a time-sensitive ask triggers a long multi-phase run with no upfront estimate.
- Token-accounting opacity: no per-phase usage estimate.
- Silent advisor conflicts: template doesn't force the Chair to surface direct contradictions.
- Executor mission creep with no rollback path when the Chair's path proves infeasible.
- Context-isolation auditing: no mechanism prevents later advisors inferring earlier findings in sequential mode.
- Reviewer scope creep can re-open the Chair's decision, creating a loop.

## Questions for the Human
1. Expected use frequency and acceptable latency for a full run?
2. How should a phase-skipping request be honored?
3. On sequential platforms, how strict is independence?
4. Who curates the appendix down to the most important advisors?
5. When the Executor hits a blocker, loop to Chair or escalate to human?

## One-line Summary
A well-architected multi-phase framework that operationally lacks affordances for lightweight usage, transparent cost/latency, observable phase attribution, and graceful degradation — prone to overuse friction and hidden token costs for casual invocations.
