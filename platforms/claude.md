# Claude / Claude Code / Cowork notes

The skill is platform-neutral, but Claude-style environments can usually execute it very well because they may support sub-agents, workspace reads, and file output.

## Recommended usage

- Import or paste `SKILL.md` as the custom skill.
- Trigger with `council this`, `develop this`, `pressure-test this`, or similar.
- If the environment supports sub-agents, run advisors in parallel.
- If it does not, run advisors sequentially but do not expose earlier responses to later advisors.

## Context files

Do not hardcode only `CLAUDE.md`. Treat it as one possible project-context file among many:

- `CLAUDE.md`
- `AGENTS.md`
- `README.md`
- `docs/`
- ADRs
- relevant source/config files
- attached files
- prior council transcripts

The Outsider must not receive any of this context.
