# Architecture

Developmental Council v3 is a modular decision-to-action framework.

The repo keeps `SKILL.md` as the platform-neutral entry point, but the behavior now lives in composable modules:

```text
core/          workflow and routing rules
packages/      domain bundles
councils/      divergent advisor sets
chairs/        convergence personalities
executors/     artifact generators
reviewers/     verification roles
templates/     report formats
```

## Why this structure

The original skill used one general-purpose council and explicitly stopped before synthesis. v3 keeps the value of divergent analysis but adds controlled convergence and optional artifact generation.

This lets the system move from:

```text
Perspectives → Briefing
```

to:

```text
Perspectives → Judgment → Artifact → Verification
```

## Core separation

- The **Council** discovers.
- The **Chair** decides what matters.
- The **Executor** creates usable outputs.
- The **Reviewer** verifies the outputs.

Each role can have domain-specific profiles without changing the core workflow.
