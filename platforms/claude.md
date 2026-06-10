# Claude / Claude Code / Cowork Notes

The skill is platform-neutral, but Claude-style environments can usually execute it well because they may support subagents, workspace reads, and file output.

## Recommended usage

- Import or paste `SKILL.md` as the custom skill.
- Keep the module files available in the workspace.
- Trigger with `council this`, `develop this`, `pressure-test this`, or similar.
- If subagents are available, run Council advisors in parallel.
- If not, run advisors sequentially but keep them isolated.

## File loading

For a writing review, load:

- `core/workflow.md`
- `packages/writing/package.md`
- `councils/writing.md`
- `chairs/editor-in-chief.md`
- optionally `executors/writing-executor.md`
- optionally `reviewers/copy-editor.md`

For engineering, use the engineering package and profiles.

## Context files

Project context may come from:

- `CLAUDE.md`
- `AGENTS.md`
- `README.md`
- `docs/`
- ADRs
- source/config files
- attached files
- prior council transcripts

Do not give enriched context to cold/outsider advisors.
