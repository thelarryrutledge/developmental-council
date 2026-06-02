# Preset: Engineering / Architecture Review

Use this configuration for technical design work: architecture decisions, API shapes, infrastructure choices, refactors, migration plans, and operational tradeoffs.

## When to use

Bring a design, not a bug. Use the council for decisions with no single obvious right answer:

- "Should this state live in Postgres, Redis, or object storage?"
- "Is this abstraction earning its keep?"
- "Will this coupling hurt in six months?"
- "How should we split these queues or services?"

Do not use it when a test, benchmark, documentation lookup, or direct code review would answer the question better.

## Seat configuration

- **Contrarian — skin: the on-call maintainer who inherits this in six months.** Argues operational reality, hidden coupling, incident risk, failure modes, and simpler shapes.
- **First-Principles** — asks what problem is actually being solved and whether the architecture created its own problem.
- **Expansionist** — looks for reusable primitives, adjacent capabilities, and the part of the design worth developing further.
- **Outsider** — receives only the bare design. Catches onboarding cliffs, implicit assumptions, and places where the design only makes sense to insiders.
- **Executor — keep.** Finds the smallest credible first step, migration path, rollout strategy, and production risk.

## Context to gather for non-Outsider advisors

- Relevant source/config/manifests.
- Architecture docs, ADRs, README files, or project-specific agent instruction files.
- Prior decisions on adjacent choices.
- Operational realities: incident history, on-call pain, deployment constraints, cost constraints.

Do not pass any of this to the Outsider.

## Audience/scope descriptor for adjudication only

Example:

> The maintainers of this system. We value explicit, operable, boring infrastructure over cleverness. This is a reversible/irreversible decision. Production reliability matters more than theoretical elegance.

## Watch-item

Contrarian and First-Principles may both argue against the design. Keep both if the reasons differ: one may be naming operational cost while the other names the wrong-problem trap.
