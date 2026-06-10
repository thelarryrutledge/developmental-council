---
developmental_council_run:
  date: 2026-06-10
  package: engineering
  scope: council+chair
  execution_mode: multi-agent
  advisor_count: 6
  advisors: [reliability, maintainability, operations, cost-complexity, product, cold-onboarder]
---

# Developmental Council Report — Re-Council of the Skill (post-cleanup)

**Subject:** `developmental-council` v3, after the honesty/onboarding/cleanup pass
**Domain:** Meta-engineering / prompt-orchestration framework
**Package:** Engineering
**Chair:** Systems Architect
**Date:** 2026-06-10
**Scope:** Council + Chair (default)
**Execution mode:** True multi-agent — 6 independent subagents (Reliability, Maintainability, Operations, Cost/Complexity, Product, Cold Onboarder), no shared context until the Chair phase. Independence is real.

---

## 1. Executive Summary

The cleanup worked — the differentiator is now well-sold, the independence claim is honest, and DP1 is genuinely closed (Product, Maintainability, Cold Onboarder all confirm). **But the pass traded one class of problem for another: it fixed honesty and added guardrails, and in doing so it (a) created a cross-file contradiction and (b) re-introduced the duplication that MF3 was meant to kill.**

The loudest signal — raised independently by **4 of 6 advisors** — is a **positioning/consistency contradiction**: the README still headlines four symmetric phases, while `core/workflow.md` + `SKILL.md` now say Council→Chair is the default and the rest is opt-in. The cleanup edited two of those three files and left the third contradicting them.

This is again a **documentation + consistency** problem, not an architectural one. Smallest credible move: one more small consistency pass. One genuine product decision (DP-A) and one scope decision (DP-B) are left for the human.

---

## 2. Controlled Convergence Report (Chair: Systems Architect)

### Where advisors agreed (strong signal)

- **The four-phase headline now contradicts the documented default.** *(From advisors: Product High, Cold Onboarder High, Cost/Complexity High; corroborated by Maintainability.)* README leads with four equal phases; SKILL/workflow say Council→Chair is the implicit default with Executor/Reviewer opt-in. A newcomer mentally commits to an expensive pipeline before learning most of it is optional.
- **The cleanup re-introduced duplication.** *(From advisors: Maintainability High, Cost/Complexity Med.)* "Controlled convergence" is now defined in both SKILL.md and README (with subtly different wording — "never collapsing" vs "rather than collapsing"); traceability lives in both `workflow.md` and the template. Single-source-of-truth (the MF3 goal) eroded.
- **Scope steering is declared but not actionable or observable.** *(From advisors: Operations High, Cost/Complexity Med, Reliability High.)* No mechanism/syntax for "reduced advisor set"; nothing records which scope/mode/advisor-count a run used.
- **The "roughly double the cost" claim is probably false.** *(From advisors: Operations High, Product Med.)* Advisors dominate token cost (6–7× generation); adding Chair/Executor/Reviewer is closer to +30%, not 2×. SF1's cost rationale rests on a shaky number.
- **README never mentions scope or cost.** *(From advisors: Maintainability Med, Product Med, Cold Onboarder Med.)* The Scope table is buried in `workflow.md`; README readers never learn the default is cheap-by-design.

### Chair synthesis (not attributable to one advisor)

- **The cleanup's pattern was "add, don't reconcile."** It added definitions, a Scope section, loop-back, traceability, and a when-to-use section — each in *a* file, without checking the *other* entry points stayed consistent. That is why both the contradiction and the duplication appeared. The fix is reconciliation, not more additions.
- **Two findings are the OPT2/SF1 features just shipped, now showing their failure modes** — traceability can be fabricated (Reliability Med), and reduced-advisor steering is a feature-shaped phrase with no mechanism (Operations Med). Either complete them or stop implying they are features.
- **The symlink set up last turn exposes `output/` and `private/`** *(From advisor: Operations Med)* — real, and install docs are silent on it.
- **The skill did not auto-produce this report as a file on the first pass** — the executing agent defaulted to chat output despite the documented Output-preference behavior. This is a live instance of "output steering declared but not enforced." (Added by Chair from observed run behavior.)

### Ranked — what matters most

**Must-fix (the cleanup genuinely introduced these):**

- **MF-a — Resolve the four-phase vs. Council→Chair contradiction.** Make README agree with SKILL/workflow: lead with (or prominently note) that Council→Chair is the default and Executor/Reviewer are opt-in.
- **MF-b — Kill the new duplication.** Pick one canonical home per concept (convergence definition; traceability rule) and have the others cross-reference it. Reconcile the two definition wordings.

**Should-fix (operability / honesty of the new features):**

- **SF-a — Fix the cost claim.** Replace "roughly double" with what is true: the *council* dominates cost; reducing advisor count is the real lever.
- **SF-b — Make traceability honest.** Add the "From advisors" vs "From synthesis" distinction to the Chair instructions + template (prevents fabricated attribution). This report demonstrates the fix.
- **SF-c — Document the symlink install** and note `output/`/`private/` exposure.
- **SF-d — Put a short scope/cost note in README** (or link the Scope table).
- **SF-e — Reinforce file-output behavior** so a run produces the report artifact by default, not only on request.

**Optional / preference:**

- **OPT-a** — Reduced-advisor selection: define it as a real mechanism or remove the implication *(Operations, Cost/Complexity)*.
- **OPT-b** — A concrete *domain* worked example (not the meta self-review) *(Product, Cost/Complexity)*.
- **OPT-c** — Sharpen the loop-back execution-vs-decision boundary *(Reliability)*.
- **OPT-d** — Cold-onboarder UX: a "how do I actually invoke this + which package" line in README/SKILL *(Cold Onboarder)*.

### Tensions preserved — human decision points

- **DP-A — Reframe the product around Council→Chair? (this is the prior DP2, returned louder.)** Three advisors independently re-derived it. **Cost/Complexity and Product** want the headline to lead with the two-phase core and demote Executor/Reviewer to optional add-ons. **Maintainability** cautions that the modular four-part structure is a must-preserve and should not be gutted. MF-a (make docs consistent) is *not* the same as DP-A (change the identity): the contradiction can be fixed by demoting the extra phases **or** by clearly labeling them optional while keeping the four-phase identity. Direction is the human's call.
- **DP-B — How much instrumentation is worth it?** Operations wants structured run metadata (YAML frontmatter: scope, mode, advisor count, cost) and an execution-mode assertion checkpoint. Real observability — but also ceremony for a markdown skill, and a possible over-engineering risk. Worth it, or overbuild?

### Groupthink check

Not groupthink. The six converged hard on the positioning contradiction but genuinely *diverged* on the remedy: Cost/Complexity pushes to **cut and simplify**, Reliability/Operations push to **add checkpoints and metadata**, Maintainability pushes to **preserve structure**. That cut-vs-add-vs-preserve tension is real and is exactly DP-A/DP-B.

### Smallest credible next move

One small consistency pass: **MF-a, MF-b, SF-a–SF-e** — all documentation, all reversible, no architectural change. Defer OPT-* and resolve **DP-A before MF-a** (the positioning choice determines *how* README is made consistent).

---

## 3. Executor Deliverable

Not run. Per the requested default scope, and because **MF-a depends on the human's DP-A decision**, no Executor plan was prepared. The Chair recommends resolving DP-A, then running the Executor on MF-a/MF-b/SF-a–SF-e as independent commits.

---

## 4. Advisor Appendix

Full independent advisor reports are in `appendices/`:

1. `01-reliability.md` — Reliability / Failure-Modes
2. `02-maintainability.md` — Maintainability
3. `03-operations.md` — Operations
4. `04-cost-complexity.md` — Cost / Complexity
5. `05-product.md` — Product / Business
6. `06-cold-onboarder.md` — Cold Onboarder

Highest-severity item per advisor:

- **Reliability (High):** scope default assumes but does not validate; loop-back conflates decision-objection with execution-failure.
- **Maintainability (High):** dual definition of "controlled convergence"; divergent when-to-use guidance across entry points.
- **Operations (High):** scope/cost steering declared but not syntactically usable or observable; cost claim likely wrong.
- **Cost/Complexity (High):** value concentrates in Council→Chair but structure signals four-phase parity; cleanup added ceremony rather than removing dead weight.
- **Product (High):** positioning contradiction (four-phase headline vs Council→Chair default); differentiator now well-sold (strength).
- **Cold Onboarder (High):** README↔SKILL contradiction on the default; "how do I actually invoke this?" gap.

---

*The council recommends and prepares; it does not decide. Final authority is yours.*
