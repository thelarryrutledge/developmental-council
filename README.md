# Developmental Council

A platform-neutral Agent Skill for structured multi-perspective review, controlled convergence, artifact creation, and verification.

Developmental Council v3 runs complex work through four phases:

```text
Council → Chair → Executor → Reviewer
```

- **Council** generates independent perspectives.
- **Chair** performs controlled convergence.
- **Executor** creates domain-appropriate artifacts.
- **Reviewer** verifies the result.

The human retains final authority.

**Controlled convergence** means ranking and reconciling divergent perspectives into prioritized, decision-ready guidance while explicitly preserving the tradeoffs that remain unresolved — rather than collapsing disagreement into a single false consensus.

## What changed in v3

Earlier versions focused on developmental critique without collapsing to a verdict. v3 keeps that divergent review step but adds a synthesis and action layer.

The goal is no longer only:

```text
What are the perspectives?
```

The goal is:

```text
What do the perspectives reveal, what should we do with them, what artifact should be prepared, and did it work?
```

## Repository structure

```text
SKILL.md                  platform-neutral entry point
core/                     workflow and routing rules
packages/                 domain bundles
councils/                 advisor sets
chairs/                   controlled-convergence personas
executors/                artifact-generation roles
reviewers/                verification roles
templates/                output formats
docs/                     architecture and extension docs
examples/                 example prompts and presets
platforms/                platform-specific notes
```

## Built-in public packages

### Writing

For essays, chapters, manuscripts, sermons, articles, arguments, and communication.

Components:

- `councils/writing.md`
- `chairs/editor-in-chief.md`
- `executors/writing-executor.md`
- `reviewers/copy-editor.md`

### Engineering

For software architecture, infrastructure, APIs, refactors, migrations, and operational tradeoffs.

Components:

- `councils/engineering.md`
- `chairs/systems-architect.md`
- `executors/engineering-executor.md`
- `reviewers/technical-validator.md`

## Install

Use this directory as the skill folder:

```text
developmental-council/
  SKILL.md
  core/
  packages/
  councils/
  chairs/
  executors/
  reviewers/
  templates/
```

The required entry point is `SKILL.md`.

If a platform cannot dynamically read the supporting files, paste the relevant package and profile files into the session along with `SKILL.md`.

## Trigger phrases

- `council this`
- `develop this`
- `pressure-test this`
- `stress-test this`
- `run the council`
- `what am I missing?`
- `poke holes in this`
- `how do I make this stronger?`
- `turn this into a plan`
- `review this and propose changes`

## Platform compatibility

The skill remains platform-neutral.

It can run with:

- parallel subagents when available
- multiple model calls when available
- isolated sequential passes when parallelism is unavailable
- chat-only output when file output is unavailable
- markdown/HTML artifacts when file output is available

The essential requirement is Council-phase independence: advisors should not see each other's outputs until the Chair phase.

## Documentation

- `docs/architecture.md`
- `docs/extension-guide.md`
- `docs/migration-v2-to-v3.md` (historical — how v2 became v3)

## Worked example

For a complete, real end-to-end run — including the raw independent advisor
reports, the Chair's convergence, the prepared plan, and the verification — see
[`examples/walkthrough-self-review/`](examples/walkthrough-self-review/). In it,
the council reviews this skill's own design.

## Lineage

This project draws from the broader LLM council pattern: dispatching a prompt through multiple independent perspectives and reviewing the responses. v3 adapts that pattern into a modular decision-to-action framework with explicit divergence, convergence, execution, and verification phases.

## License

MIT — see `LICENSE`.
