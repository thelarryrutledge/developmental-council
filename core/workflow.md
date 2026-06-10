# Core Workflow

Developmental Council v3 runs four phases.

```text
Council → Chair → Executor → Reviewer
```

The core workflow is domain-neutral. Domain-specific behavior lives in packages, councils, chairs, executors, and reviewers.

## Scope — how much of the pipeline to run

The full four-phase pipeline is the *maximum*, not the default. Most runs should stop at the Chair.

| Scope | Phases run | When to use |
|---|---|---|
| **Default** | Council → Chair | The implicit default. Use when the user wants perspectives and a converged recommendation: "council this", "what am I missing?", "pressure-test this". |
| **Full pipeline** | Council → Chair → Executor → Reviewer | Use only when the user asks for artifacts, a plan, code, revisions, or "the whole thing": "turn this into a plan", "run the full council", "and implement it". |
| **Review only** | Council | Use when the user explicitly wants raw perspectives without convergence. |

The Executor and Reviewer roughly double the work and token cost of a run, which is why they are opt-in. Add them when the user wants something built or verified — not by default.

Advisor count is also adjustable: run the package's full council by default, but honor an explicit request for a reduced set (e.g. "just the robustness and operations lenses") to keep a run cheap and fast.

If scope is ambiguous, assume **Default** (Council → Chair) and offer to continue to the Executor/Reviewer rather than running them unprompted.

## Phase 0 — Frame the brief

Create a neutral brief before running any advisor.

Include:

- artifact, decision, or problem
- domain
- stakes
- known constraints
- user goal
- audience/scope, if relevant
- requested output level: review only, convergence, artifacts, or full workflow

Ask at most one clarifying question only when the input is too ambiguous to proceed. If enough is available, proceed.

## Phase 1 — Council

Purpose: generate diverse independent perspectives.

Rules:

- Run advisors independently.
- Do not let advisors see each other's reports.
- Give each advisor only the context appropriate to that role.
- Require structured findings.
- Do not ask advisors to synthesize or decide.

Advisor output should use `templates/advisor-report.md`.

## Phase 2 — Chair

Purpose: controlled convergence.

The Chair receives:

- neutral brief
- structured advisor reports
- optional gap observations
- audience/scope
- user constraints

The Chair must:

- identify agreement
- identify disagreement
- rank what matters
- distinguish must-fix from optional preference
- preserve unresolved tensions
- name human decision points
- recommend a path forward
- attribute each finding to the advisor lens(es) that raised it, so the reader can trace any recommendation back to its source

The Chair should not pretend consensus exists where it does not.

Chair output should use `templates/convergence-report.md`.

## Phase 3 — Executor

Purpose: create domain-appropriate artifacts from the Chair's guidance.

The Executor receives:

- neutral brief
- Controlled Convergence Report
- explicit constraints
- optionally the advisor appendix

The Executor may produce:

- rewritten text
- outlines
- architecture plans
- implementation checklists
- code patches or PR drafts
- decision matrices
- roadmaps
- itineraries

The Executor operates within the Chair's recommended path. It should not re-litigate the decision unless it finds an execution blocker.

Skip this phase if the user asked only for analysis.

## Phase 4 — Reviewer

Purpose: verify the Executor output.

The Reviewer receives:

- neutral brief
- Controlled Convergence Report
- Executor deliverables
- relevant constraints

The Reviewer validates:

- alignment with Chair recommendations
- correctness
- completeness
- quality
- missing risks
- unintended consequences

Reviewer output should use `templates/verification-report.md`.

### When the Reviewer says "Needs revision"

This only applies in the full pipeline (where an Executor produced something to verify).

- Run **at most one** revision cycle: hand the Reviewer's findings back to the Executor, which revises within the Chair's recommended path, then the Reviewer re-checks.
- If the second pass still fails, **stop and escalate to the human** — report the unresolved issue and the disagreement rather than looping again. Never run unbounded revision cycles.
- If the Reviewer's objection is really with the Chair's decision (not the execution of it), do not revise — surface it to the human as a decision point.

## Final assembly

Produce:

1. Executive summary
2. Controlled Convergence Report
3. Executor Deliverables, if any
4. Reviewer Assessment, if any
5. Advisor Appendix

The primary report should be concise. Appendices may be detailed.
