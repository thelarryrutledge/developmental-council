# Advisor Appendix — Product / Purpose

**Lens:** Does this solve a real problem better than alternatives, and for whom?
**Design-health score (Chair estimate):** 62 / 100

## Role
Product advisor assessing whether the skill solves a real user problem better than alternatives, and for whom.

## Top Findings

1. **Problem solved: Structured divergence-before-convergence for complex judgment** — forcing divergence early prevents premature consensus; the Council isolation rule is hard to reproduce ad-hoc. **Severity: High (strength)**

2. **Modularity is overbuilt relative to current deployment** — two packages plus an extensibility system, but only two domains; ceremony can feel heavy for a one-off user. **Severity: Med**

3. **Job-to-be-done clarity gap: when is this better than "Claude, poke holes in this?"** — no concrete expectation of outcome difference (more insightful? longer? less prescriptive?). **Severity: Med**

4. **Human authority framing is protective but reads like a compliance disclaimer** — doesn't answer the user's real question, "should I follow the recommendation?" **Severity: Low**

5. **The Executor–Reviewer loop may not be the real value; the Chair is** — symmetric four-phase framing over-suggests ceremony; ~80% of value may be the synthesis. **Severity: Med**

6. **Differentiation vs. existing multi-agent review patterns is underspecified** — no clear signal for when to choose this over `code-review` / `plan_review` / parallel review workflows. **Severity: Med**

7. **The "preserved disagreement" philosophy is distinctive and underrated** — preserving tension instead of collapsing it is the genuine differentiator and is buried as a philosophical aside. **Severity: High (strength)**

## Risks & Blind Spots
- Overestimation of Council value: no evidence isolated advisors beat advisors who see each other.
- Downstream skew: expensive verification on outputs the user already doubts.
- No cost-vs-value guidance for the ~4× token cost.
- Writing vs engineering workflows differ (iterative vs once-through) but packages aren't tailored to that.
- "Controlled convergence" is jargon used 20+ times but never defined.

## Questions for the Human
1. What's the primary problem this solves that existing review skills don't?
2. Is the Chair the real blocker users face — and should the product center on it?
3. Who is the target user: solo thinker or team facilitator?
4. How should this compete with "just ask Claude to poke holes"?
5. Expected token cost, and when is it worth it?

## One-line Summary
Solves a real but narrow problem (preserving disagreement + forcing independent perspectives) with a four-phase framework that reads overengineered for its core value, lacks clarity on when to use it vs. alternatives, and positions its main strength as an aside rather than the lead.
