# Codex / OpenAI-style skill runner notes

Use the standard folder layout:

```text
developmental-council/
  SKILL.md
```

The skill frontmatter is standard YAML:

```yaml
---
name: developmental-council
description: ...
---
```

Codex-style runners can use the skill when the user's request matches the trigger language or when the task clearly benefits from multi-perspective developmental critique.

If parallel execution is unavailable, simulate independence with isolated sequential passes and keep each advisor blind to prior advisor outputs until the gap pass.
