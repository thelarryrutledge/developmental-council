---
name: developmental-council
description: Run a substantive idea, draft, design, architecture, strategy, or decision through a modular Council → Chair → Executor → Reviewer workflow. Use when the user asks to council, develop, pressure-test, stress-test, poke holes in, strengthen, review, synthesize, create an implementation plan, or turn a complex set of perspectives into controlled convergence and actionable artifacts. Do not use for simple factual lookup, pure creation with no review need, trivial yes/no choices, or low-stakes decisions with no meaningful tradeoff.
---

# Developmental Council

Developmental Council is a platform-neutral agent skill for structured multi-perspective review and controlled convergence.

The v3 architecture separates four responsibilities:

1. **Council** — generates independent perspectives.
2. **Chair** — performs controlled convergence.
3. **Executor** — creates domain-appropriate artifacts from the Chair's decision.
4. **Reviewer** — verifies the Executor's work against the Chair's guidance.

The human retains final authority. The skill should improve judgment and execution quality without pretending the system has the final word.

## Core operating rule

Do not collapse perspectives too early.

Run divergence first, then convergence, then artifact creation, then verification:

```text
Council → Chair → Executor → Reviewer
```

## File loading

When the host platform supports workspace/file reads, load these files as needed:

- `core/workflow.md` — canonical workflow.
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

## Required behavior

1. Frame a neutral brief.
2. Select or build the package.
3. Run Council advisors independently.
4. Run the Chair over structured advisor findings.
5. Run the Executor only when the user wants artifacts, revisions, plans, code, PR drafts, checklists, or next-step outputs.
6. Run the Reviewer when Executor output exists or when correctness matters.
7. Produce the final report with advisor appendix.

## Independence requirement

Council advisors must not see each other's outputs. If parallel subagents are unavailable, simulate independence by running isolated sequential passes and not exposing earlier responses to later advisors.

The Chair, Executor, and Reviewer may see prior phase outputs.

## Output preference

Prefer a concise primary report with appendices.

The user should be able to act from the Controlled Convergence Report without reading every advisor report. Full advisor reports should be included as supporting evidence, not the primary product.

When file output is available, create:

- `developmental-council-report-[timestamp].md`
- optional `developmental-council-report-[timestamp].html`

## Human authority

Never imply the council has made the final human decision. The Chair may recommend, the Executor may prepare, and the Reviewer may verify, but the human decides what to accept.
