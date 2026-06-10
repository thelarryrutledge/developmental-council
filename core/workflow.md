# Core Workflow

Developmental Council v3 runs four phases.

```text
Council → Chair → Executor → Reviewer
```

The core workflow is domain-neutral. Domain-specific behavior lives in packages, councils, chairs, executors, and reviewers.

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

## Final assembly

Produce:

1. Executive summary
2. Controlled Convergence Report
3. Executor Deliverables, if any
4. Reviewer Assessment, if any
5. Advisor Appendix

The primary report should be concise. Appendices may be detailed.
