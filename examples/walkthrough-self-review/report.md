# Developmental Council Report — The Council Reviews Itself

**Subject:** `developmental-council` v3 skill (its own design/architecture)
**Domain:** Meta-engineering / prompt-orchestration framework
**Package:** Engineering (advisor lenses adapted to a prompt framework)
**Date:** 2026-06-10
**Workflow run:** Council (6 advisors, independent) → Chair → Executor → Reviewer

---

## 1. Executive Summary

The four-phase architecture (Council → Chair → Executor → Reviewer) is conceptually sound and its most distinctive virtue — *preserving disagreement instead of collapsing it* — is real and rare. The problems are not architectural; they are **honesty, surface area, and onboarding** problems:

1. The headline claim (independent advisors) is **unverifiable and leaky** when one model runs everything sequentially. This very run mitigated it by using six separate subagents — but the skill never tells you that's required, nor what to do when it isn't possible.
2. The core term **"controlled convergence" is never defined**, and there is **no end-to-end worked example** — the two things a newcomer needs most.
3. There is **measurable dead/duplicated surface area**: SKILL.md duplicates `core/workflow.md`; `private/` is referenced but absent; v2 artifacts are orphaned.
4. There is **no lightweight path and no steering** — every invocation implies the full, expensive pipeline, with no documented way to say "Council + Chair only."

**Recommended path:** A single documentation-and-cleanup pass (no architectural rewrite). It is reversible, high-leverage, and addresses every High-severity finding. Two genuine tensions are left for **you** to decide (independence investment; pipeline scope).

---

## 2. Controlled Convergence Report (Chair: Systems Architect)

### Where the advisors agreed (strong signal)

- **Independence is asserted but not guaranteed.** Robustness, Operations, and Cold Onboarder all flag that single-model sequential execution leaks context and collapses perspectives, while the docs describe the *principle* of isolation but no *mechanism* or *self-check*.
- **The framework under-explains itself.** "Controlled convergence" undefined (Cold Onboarder, Product); no worked example with real output (Cold Onboarder, Maintainability, Complexity); package/file layout unclear to newcomers.
- **There is dead and duplicated surface.** SKILL.md ↔ `core/workflow.md` duplication (Maintainability, Complexity); `private/` declared but absent (Maintainability, Cold Onboarder, Complexity); orphaned v2 migration references (Complexity, Maintainability).
- **No proportionate / lightweight mode.** Full pipeline cost is high; no phase-skip syntax, no advisor-count control, no default "lite" path (Operations, Product, Complexity).
- **No loop-back semantics.** If the Reviewer says "Needs revision," the linear workflow has no defined next step (Robustness, Operations).

### Ranked — what matters most

**Must-fix (the framework currently claims more than it can guarantee):**

- **MF1 — Make independence honest.** Document that true independence requires separate agent/model invocations; describe the degraded-but-labeled fallback explicitly; add a Chair self-check ("if advisors converged completely, flag possible groupthink rather than report false consensus").
- **MF2 — Define "controlled convergence"** in one sentence in README and SKILL.md.
- **MF3 — Single source of truth** for the workflow: SKILL.md summarizes and *points to* `core/workflow.md`; stop maintaining the phase logic twice.
- **MF4 — Resolve dead references:** create or delete `private/`; archive or clearly mark the v2 migration doc.

**Should-fix (operability and demonstrated value):**

- **SF1 — Lightweight path + steering.** Make Council+Chair the implicit default; document how to request review-only, full-pipeline, or a reduced advisor set. State the rough cost tradeoff.
- **SF2 — One end-to-end worked example** with abbreviated real outputs for each phase.
- **SF3 — Reviewer loop-back rule:** one bounded revision cycle, then escalate to the human (no unbounded loops).
- **SF4 — "When to use this vs. alternatives"** short section (vs. just asking; vs. `code-review`/`plan_review`); lead with the preserved-disagreement differentiator.

**Optional / preference (do not over-rotate):**

- **OPT1 — Trim/consolidate** redundant `core/` files and near-identical templates *only if* it doesn't hurt the extension story (Maintainability values them).
- **OPT2 — Finding traceability** back to advisors in the final report.
- **OPT3 — Concrete "do not run" rubric** (stakes/tradeoff thresholds).

### Tensions preserved — human decision points

- **DP1 — Independence: invest or soften?** Either commit to real multi-call isolation (and require it) *or* downgrade the claim from "independent" to "distinct-lens" perspectives. Don't keep marketing a guarantee the common execution path can't keep.
- **DP2 — Pipeline scope.** Complexity and Product suspect most value lives in Council→Chair and that Executor/Reviewer are speculative. They are *already* optional in the docs — the question is whether to **reframe the product around the Chair** (with execution as an add-on) or keep the symmetric four-phase identity.
- **DP3 — Modularity vs. overbuild.** Maintainability calls the structure sound; Complexity calls 24 files overbuilt for two domains. Resolution: structure stays, but **add no new modules until a third domain actually exists**, and remove what's genuinely dead.

### Smallest credible next move

One documentation + cleanup PR covering MF1–MF4, SF1–SF4. No code/architecture rewrite. Fully reversible.

---

## 3. Executor Deliverable — Strengthening Plan (Engineering Executor)

Prepared but **not applied** — the human decides what to accept. Proposed as small reviewable units.

**Unit A — Honest independence (MF1, DP1)**
- `SKILL.md` "Independence requirement": add that genuine independence = separate subagent/model invocations; the sequential fallback yields *labeled* "distinct-lens" perspectives, not guaranteed independence.
- `chairs/*.md`: add behavior — "If advisors converge on everything, report possible groupthink/insufficient diversity rather than manufacture consensus or fabricate disagreement."

**Unit B — Define the term + worked example (MF2, SF2)**
- `README.md` + `SKILL.md`: one-line definition of "controlled convergence" (e.g., *"ranking and reconciling divergent perspectives into prioritized, decision-ready guidance while explicitly preserving unresolved tradeoffs"*).
- `examples/`: add `engineering-walkthrough.md` showing brief → 2 abbreviated advisor snippets → Chair excerpt → Executor excerpt → Reviewer verdict.

**Unit C — De-duplicate workflow (MF3)**
- `SKILL.md` "Required behavior": collapse to a short summary that defers to `core/workflow.md` as authoritative.

**Unit D — Dead references (MF4)**
- Remove `private/` from `README.md` + `docs/architecture.md`, or add `private/.gitkeep` + a one-line README. Mark `docs/migration-v2-to-v3.md` as historical or move to `docs/history/`.

**Unit E — Steering + lite path (SF1)**
- `SKILL.md` "Required behavior": document default = Council+Chair; opt-in Executor/Reviewer; allow reduced advisor count; note cost tradeoff in one line.

**Unit F — Loop-back + when-to-use (SF3, SF4)**
- `core/workflow.md` Phase 4: add bounded one-cycle revision then human escalation.
- `README.md`: short "When to use vs. alternatives," leading with preserved-disagreement.

Suggested order: A, C, D (correctness/cleanup) → B, E, F (clarity/UX). Each is an independent commit.

---

## 4. Reviewer Assessment (Technical Validator)

**Verdict: Pass with reservations.**

- **Alignment:** Plan maps 1:1 to every Must-fix and Should-fix; no Chair recommendation dropped. ✓
- **Correctness:** Edits are documentation/structure only — low blast radius, reversible, no behavioral risk to running workflows. ✓
- **Completeness gaps (reservations):**
  - DP1/DP2/DP3 are correctly left as human decisions, but **Unit A partially pre-commits** to the "soften the claim" side of DP1. Flag explicitly so the human chooses *soften vs. invest* before merging A.
  - Units B and F overlap (worked example + "when to use") — fine, but verify the example reflects whatever default is chosen in Unit E so docs don't contradict.
  - No unit addresses OPT2 (traceability); acceptable to defer, but note it.
- **Unintended consequences:** Removing `private/` references is safe *only if* no private profiles are in use elsewhere — confirm before deleting (prefer `.gitkeep` if unsure).

**Recommendation:** Proceed with C/D first (pure cleanup), resolve DP1 before A, then B/E/F.

---

## 5. Advisor Appendix

Full independent advisor reports (Robustness, Maintainability, Operations, Product, Complexity, Cold Onboarder) are retained in the session transcript. Highest-severity items per advisor:

- **Robustness (High):** single-model "independence" is theater; Chair may fabricate or smooth consensus; cross-phase context leakage.
- **Maintainability (Med):** SKILL.md/workflow.md duplication; no test/acceptance harness for prompt behavior; `private/` absent.
- **Operations (High):** disproportionate token cost; no lightweight/steering path; output digestibility risk.
- **Product (High strength):** preserved-disagreement is the true differentiator and is under-sold; value may concentrate in the Chair phase.
- **Complexity (High):** v2→v3 expansion may be scope creep; 24 files for two domains; no evidence Executor/Reviewer are needed beyond Council→Chair.
- **Cold Onboarder (High):** "controlled convergence" undefined; no end-to-end worked example; package/file layout unclear; independence requirement buried.

---

*The council recommends and prepares; it does not decide. Final authority is yours.*
