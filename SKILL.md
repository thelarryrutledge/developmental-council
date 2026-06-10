---
name: counterpoint
description: Run a substantive idea, draft, design, architecture, strategy, or decision through a modular Council → Chair → Executor → Reviewer workflow. Use when the user asks to council, develop, pressure-test, stress-test, poke holes in, strengthen, review, synthesize, create an implementation plan, or turn a complex set of perspectives into controlled convergence and actionable artifacts. Do not use for simple factual lookup, pure creation with no review need, trivial yes/no choices, or low-stakes decisions with no meaningful tradeoff.
---

# Counterpoint

Counterpoint is a platform-neutral agent skill for structured multi-perspective review and controlled convergence.

*Controlled convergence* means ranking and reconciling divergent perspectives into prioritized, decision-ready guidance while explicitly preserving the tradeoffs that remain unresolved — never collapsing disagreement into a single false consensus. (`core/workflow.md` Phase 2 is the canonical definition.)

The core of the skill is two phases:

1. **Council** — generates independent perspectives.
2. **Chair** — performs controlled convergence (ranks them, preserves real tradeoffs, recommends a path).

This is the default and the product. Two further phases are **optional add-ons that make the Chair's recommendation actionable**, run only on explicit request:

3. **Executor** — turns the Chair's recommendation into artifacts (plan, code, revisions, PR draft).
4. **Reviewer** — verifies the Executor's work against the Chair's guidance.

The human retains final authority. The skill should improve judgment and execution quality without pretending the system has the final word.

## Core operating rule

Do not collapse perspectives too early. Run divergence first, then convergence:

```text
Council → Chair          (default — the product)
```

When the user asks to make the recommendation actionable, extend with:

```text
→ Executor → Reviewer    (opt-in — artifacts and verification)
```

## File loading

When the host platform supports workspace/file reads, load these files as needed:

- `core/workflow.md` — canonical workflow (phases, scope, run metadata).
- `core/package-selection.md` — how to route a brief to the right package.
- `core/context-isolation.md` — what context each phase may see (the isolation matrix).
- `packages/<domain>/package.md` — domain routing and defaults.
- `councils/<name>.md` — advisor definitions.
- `chairs/<name>.md` — synthesis personality and priorities.
- `executors/<name>.md` — artifact-generation behavior.
- `reviewers/<name>.md` — verification behavior.
- `templates/*.md` — output templates.

If the platform cannot load files dynamically, treat the included markdown files as instruction modules and paste the relevant modules into the active session.

## Default public packages

Use these built-in packages unless the user asks for a custom configuration:

| Domain | Package |
|---|---|
| Writing, editing, manuscripts, arguments | `packages/writing/package.md` |
| Engineering, architecture, infrastructure, refactors | `packages/engineering/package.md` |

If no package fits, run the generic workflow in `core/workflow.md` and build a temporary council/chair/executor/reviewer from the user's domain.

## When to run

Run this skill for substantive artifacts or genuinely uncertain problems where multiple perspectives and controlled convergence would help.

Good triggers:

- `council this`
- `develop this`
- `pressure-test this`
- `stress-test this`
- `run the council`
- `what am I missing?`
- `poke holes in this`
- `how do I make this stronger?`
- `turn this feedback into a plan`
- `review this and tell me what to change`

Do not run it for:

- simple factual lookups
- direct calculations
- trivial implementation questions
- low-stakes choices
- requests where a normal answer would be clearer

## Default flow and optional extensions

`core/workflow.md` is the authoritative description of the phases. At a glance:

**Default flow — always:**

1. Frame a neutral brief.
2. Select or build the package.
3. Run the Council, then the Chair. Stop here and produce the report — this is what "council this" means.

**Optional extensions — only on explicit request** (e.g. "a full council," "council with execution," "turn this into a plan," or a follow-up to "make the recommendation actionable"):

4. Run the Executor to turn the Chair's recommendation into artifacts.
5. Run the Reviewer to verify the Executor's work.

**Always, in either case:** produce the report files (markdown + HTML + advisor appendices), per Output preference below.

For phase-by-phase rules, context isolation, and final assembly, follow `core/workflow.md` rather than this summary.

## Independence requirement

Council advisors must not influence each other during the Council phase. How fully that holds depends on how the skill is sourced — be explicit about which mode produced a report:

- **True multi-agent execution** (Claude Code, Codex, or any host that can spawn parallel subagents or make separate model calls): each advisor runs as a genuinely isolated agent with its own context. Independence is real.
- **Single-session execution** (one model, no subagent support): advisors are distinct *personas* run as isolated sequential passes inside one context. This approximates independence but does not guarantee it — earlier reasoning can bias later personas. Treat these as "distinct-lens" perspectives, not provably independent ones.

In either mode, do not expose one advisor's output to another during the Council phase. Always state which mode was used so the reader can calibrate how independent the perspectives actually are. Never present single-session persona passes as if they were fully isolated agents.

The Chair, Executor, and Reviewer may see prior phase outputs; isolation only matters during the Council phase.

## Output preference

Prefer a concise primary report with appendices.

The user should be able to act from the Controlled Convergence Report without reading every advisor report. Full advisor reports should be included as supporting evidence, not the primary product.

When file output is available, **produce the report as files by default** — do not wait to be asked. A run's deliverable is the artifact, not a chat dump; keep the chat reply to a concise summary plus next steps that point at the file. Create:

- `counterpoint-report-[timestamp].md` — always; begins with a YAML run-metadata block (see `core/workflow.md` → Final assembly) so runs can be analyzed across time
- `counterpoint-report-[timestamp].html` — the styled artifact (design-health chart, severity tags, and an in-browser viewer for the advisor appendices); produce it by default when file output is available
- `appendices/` — one markdown file per advisor report

Write these under a `counterpoint-reports/[timestamp]/` directory in the working project (not `output/`, which many projects already use for their own build artifacts). Only fall back to chat-only output when file output is genuinely unavailable.

## Human authority

Never imply the council has made the final human decision. The Chair may recommend, the Executor may prepare, and the Reviewer may verify, but the human decides what to accept.
