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

Cost is dominated by the **Council**: each advisor is an independent generation, so a 6–7 advisor council is the largest single expense in a run. The Chair, Executor, and Reviewer each add a smaller increment on top. This has two consequences:

- The biggest lever on cost is **advisor count**, not which later phases run. Run the package's full council by default, but honor an explicit request for a reduced set (e.g. "just the reliability and operations lenses") to make a run substantially cheaper and faster.
- Adding the Executor and Reviewer increases cost moderately (not a full doubling), so they are opt-in mainly because most runs do not need an artifact or verification — add them when the user wants something built or checked.

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
- requested advisor set, if any (see below)

Ask at most one clarifying question only when the input is too ambiguous to proceed. If enough is available, proceed.

### Advisor selection

By default, run the package's full council. To run a reduced set:

- If the user names specific advisors or lenses (e.g. "just the reliability and operations lenses", "skip the cost advisor"), run exactly that set and record it in the brief.
- If the user names no advisors, run the full council.
- If a named advisor does not exist in the package, do not silently substitute — ask which lens they meant, or proceed with the closest existing lens and say so.

Record the resolved advisor set in the run metadata so reduced runs are auditable.

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

**Controlled convergence** (canonical definition): ranking and reconciling divergent perspectives into prioritized, decision-ready guidance while explicitly preserving the tradeoffs that remain unresolved — never collapsing disagreement into a single false consensus. (README.md and SKILL.md echo this one-liner; this is the source.)

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
- attribute each finding honestly (see traceability rule below)

The Chair should not pretend consensus exists where it does not.

### Traceability — attribute findings honestly

Each finding should be traceable, but do not fabricate sourcing. Label every finding as one of:

- **From advisors** — name the advisor lens(es) that actually raised it (e.g. "Reliability, Operations"). Only list an advisor that genuinely raised the point.
- **From synthesis** — the Chair's own observation, derived by combining or ranking advisor inputs rather than stated by any single advisor. Mark it as synthesis instead of inventing an advisor source.

This keeps the report honest about where evidence ends and the Chair's judgment begins. Never attribute a synthesis insight to an advisor who did not raise it.

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

To classify an objection, apply this test:

- **Execution problem → revise** (one cycle): the deliverable violates a stated Chair recommendation, contains a technical/logical error, or omits something the Chair asked for.
- **Decision problem → escalate** (do not revise): the objection is "the Chair's chosen path is itself wrong" — the deliverable faithfully executes the recommendation, but the Reviewer disputes the recommendation.

When genuinely unsure which it is, escalate rather than revise — looping on a decision the Chair already made wastes cycles and can erode the Chair's preserved tradeoffs.

## Final assembly

Produce:

1. Run metadata (see below)
2. Executive summary
3. Controlled Convergence Report
4. Executor Deliverables, if any
5. Reviewer Assessment, if any
6. Advisor Appendix

The primary report should be concise. Appendices may be detailed.

### Run metadata

Begin the markdown report with a structured metadata block (YAML frontmatter) so runs can be compared and analyzed across time. This is the machine-readable record of how the run was configured:

```yaml
---
developmental_council_run:
  date: YYYY-MM-DD
  package: engineering        # or writing, or a custom package name
  scope: council+chair        # council-only | council+chair | full-pipeline
  execution_mode: multi-agent # multi-agent | single-session
  advisor_count: 6
  advisors: [reliability, maintainability, operations, cost-complexity, product, cold-onboarder]
---
```

Keep it accurate, not aspirational: `execution_mode` must reflect what actually ran (true isolated agents vs. sequential personas), and `advisors` must list the set that actually ran. The HTML report does not need the raw block — its header chips already convey scope, advisor count, and mode for human readers.
