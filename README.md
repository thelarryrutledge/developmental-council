# Developmental Council

A platform-neutral Agent Skill that runs an idea, draft, design, architecture, strategy, or decision through independent advisor stances, then organizes what they found into a briefing you act on **without collapsing to a single verdict**.

This is a **developmental** council, not a **convergent** one.

- A **convergent council** tests an idea and produces a verdict.
- A **developmental council** strengthens an artifact by surfacing distinct perspectives, preserving tensions, and stopping before synthesis.

The disagreements and gaps are the product. The author decides what to do with them.

## What it does

1. Frames the artifact neutrally and gathers just enough context to ground the review.
2. Runs independent advisor passes:
   - **Contrarian** — what will fail, what is missing, what is being avoided.
   - **First-Principles** — are we solving the right problem?
   - **Expansionist** — what is strong, underdeveloped, or bigger than it looks?
   - **Outsider** — reacts with zero context to catch curse-of-knowledge issues.
   - **Executor** — optional; what happens Monday morning?
3. Runs a gap pass over anonymized advisor responses: what did everyone miss?
4. Optionally adjudicates the feedback into converge / clash / gaps / merit / mistaken / out-of-scope / strengthening.
5. Produces a scannable briefing and, where supported, an HTML report plus markdown transcript.

## Platform compatibility

The core skill is just `SKILL.md` with standard YAML frontmatter and markdown instructions. It is intentionally not tied to Claude, Claude Code, Cowork, Codex, Cursor, Copilot, Gemini CLI, or any one agent runtime.

Different platforms can execute it differently:

- Parallel sub-agents when available.
- Multiple model calls when available.
- Isolated sequential passes when parallelism is unavailable.
- Inline chat-only reports when file output is unavailable.
- HTML/markdown artifacts when file output is available.

The essential requirement is independence: advisors should not see one another's outputs until the gap pass.

## Install

### Generic Agent Skills layout

Use this directory as the skill folder:

```text
developmental-council/
  SKILL.md
  README.md
  examples/
  platforms/
```

The only required file is `SKILL.md`.

### OpenAI Codex / Codex-style skill runners

Place the `developmental-council` folder wherever your runner loads skills from. The required entry point is:

```text
developmental-council/SKILL.md
```

### Claude / Claude Code / Cowork

Import or paste the contents of `SKILL.md` as a custom skill. Claude-specific notes are in `platforms/claude.md`.

### Cursor / Copilot / Gemini / other agents

Use `SKILL.md` as a reusable instruction file or custom agent rule. If the platform does not support skill discovery directly, paste the skill body into the agent's custom instructions for the session.

## Trigger phrases

- `council this`
- `develop this`
- `pressure-test this`
- `stress-test this`
- `run the council`
- `what am I missing?`
- `poke holes in this`
- `how do I make this stronger?`

## Important design choices

| Choice | Why |
|---|---|
| No final verdict | Generative work benefits from preserved tensions. |
| No ranking | Ranking advisor outputs can introduce self-preference bias and collapses developmental value. |
| Context-starved Outsider | The Outsider only works if it does not inherit insider knowledge. |
| Audience-blind advisors | Audience context can make advisors self-censor. Only adjudication sees audience/scope. |
| Report, don't prescribe | The council gives information about the artifact, not a replacement artifact. |
| No-dismiss-for-comfort guardrail | Valid, in-scope, uncomfortable observations are often the most valuable ones. |

## Examples

See:

- `examples/engineering-preset.md`
- `examples/life-decision-preset.md`

## Lineage

This skill draws from the broader LLM council pattern: dispatching a prompt through multiple independent perspectives, reviewing the responses, and synthesizing the results. It differs from convergent council designs by removing the final verdict and focusing on developmental feedback.

Credit for the multi-perspective council lineage belongs to Andrej Karpathy's LLM Council work and Ole Lehmann's Claude-oriented LLM Council skill. This repo adapts that machinery for developmental critique rather than verdict production.

## License

MIT — see `LICENSE`.
