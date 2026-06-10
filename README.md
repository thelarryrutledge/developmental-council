# Developmental Council

A platform-neutral Agent Skill for structured multi-perspective review and controlled convergence.

At its core, the council runs two phases:

```text
Council → Chair
```

- **Council** generates independent perspectives.
- **Chair** performs controlled convergence — ranks them, preserves the real tradeoffs, and recommends a path.

**This is the default.** Asking to "council this" runs Council → Chair and returns a recommendation. That is the product.

When you want the Chair's recommendation made *actionable*, opt into two more phases:

```text
Council → Chair → Executor → Reviewer
```

- **Executor** turns the recommendation into artifacts — a plan, code, revisions, a PR draft.
- **Reviewer** verifies that work against the Chair's guidance.

Trigger these by asking for "a full council," "council with execution," or a follow-up to "make the recommendation actionable." See [`core/workflow.md`](core/workflow.md) for scope and cost.

Either way — default or full — a run produces the report files, including the styled HTML report. The human retains final authority.

**Controlled convergence** means ranking and reconciling divergent perspectives into prioritized, decision-ready guidance while explicitly preserving the tradeoffs that remain unresolved — never collapsing disagreement into a single false consensus. *(Canonical definition: [`core/workflow.md`](core/workflow.md), Phase 2.)*

## When to use this

The council's distinctive value is **preserving disagreement**: it runs independent perspectives, then converges *without* faking consensus, and hands you the unresolved tradeoffs as explicit decision points. Reach for it when that is what you need.

- **vs. just asking the model.** For a quick fact, a calculation, or a low-stakes choice, ask directly — the council is slower and more expensive by design. Use it when the work is substantive and a single confident answer would paper over real tradeoffs.
- **vs. `code-review`, `plan_review`, and similar.** Those find problems in a single artifact from one viewpoint. The council instead generates *multiple independent* viewpoints and reconciles them, surfacing where good arguments genuinely conflict.

Good fits: architecture and design decisions, strategy, drafts and arguments, plans with real tradeoffs, "what am I missing?" pressure-tests.

Skip it for: simple lookups, direct calculations, trivial implementation questions, low-stakes choices, or anything where a normal answer is clearer. A rough rule — if there is no meaningful tradeoff and no real cost to being wrong, don't run the council.

## How to invoke

Trigger the skill with a phrase like `council this` and the thing you want examined. You don't pick the internals — the skill frames a brief, selects a package, and runs the phases.

```text
council this architecture proposal: <paste or link the design>
```

What comes back: a **Controlled Convergence Report** — an executive summary, the ranked findings (where advisors agreed, what's must-fix vs. optional), and the unresolved tradeoffs left as explicit decision points for you. When file output is available you also get a styled HTML report and the raw advisor appendices.

**Which package runs:** the skill picks by domain — writing/editing/arguments → Writing; architecture/infrastructure/code/refactors → Engineering; anything else → a generic council built for your domain. To steer it, say so (e.g. "use the engineering package", or "just the reliability and operations lenses").

To go further than the default, ask for it: "…and turn it into a plan" or "run the full council" adds the Executor (artifacts) and Reviewer (verification).

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

### Installing as a symlink (for development)

To keep the installed skill in sync with a working copy, symlink it to the repo instead of copying:

```sh
ln -s /path/to/developmental-council ~/.claude/skills/developmental-council
```

Two things to know when you do this:

- The skill folder then also exposes `output/` (gitignored run artifacts) and `private/` (gitignored local profiles). That is harmless — the skill never loads `output/`, and `private/` is intentional — but do not store secrets in `private/` expecting the skill folder to hide them.
- Because `output/` and `private/` are gitignored, a clean `git status` does not mean the skill folder is empty; run artifacts accumulate under `output/`.

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
