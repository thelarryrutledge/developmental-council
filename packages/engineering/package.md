# Package: Engineering

Use this package for software architecture, infrastructure, APIs, refactors, migrations, scaling plans, reliability work, and implementation strategy.

## Components

- Council: `councils/engineering.md`
- Chair: `chairs/systems-architect.md`
- Executor: `executors/engineering-executor.md`
- Reviewer: `reviewers/technical-validator.md`

## Default workflow

1. Run Engineering Council.
2. Run Systems Architect Chair.
3. If user wants implementation artifacts, run Engineering Executor.
4. If artifacts are produced, run Technical Validator.
5. Produce final report with advisor appendix.

## Package-specific guidance

- Prefer operationally boring solutions when tradeoffs are close.
- Separate decision quality from implementation detail.
- Do not invent repository facts. Inspect files when available.
- For code changes, produce small reviewable units.
