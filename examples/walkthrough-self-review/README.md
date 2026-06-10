# Worked Example — The Council Reviews Itself

A real, end-to-end run of the Developmental Council, captured verbatim from its
first execution. The subject under review is the `developmental-council` v3 skill
*itself*, so this doubles as a demonstration and as a self-applied audit.

Use it to see what each phase actually produces before you run your own.

## The brief that started the run

```text
Run the Developmental Council engineering package on this skill's own design.

Subject: the developmental-council v3 skill (its architecture and docs).
Goal: find honesty, surface-area, and onboarding problems.

Output requested:
- Controlled Convergence Report
- a strengthening plan (prepared, not applied)
- technical validation of that plan
```

## How it ran

Council (6 independent advisors) → Chair → Executor → Reviewer.

Each advisor ran as a separate subagent so the perspectives were genuinely
independent — exactly the condition the report itself flags as required for the
"independence" claim to hold.

## How to read these files

| File | Phase | What it shows |
|------|-------|---------------|
| [`report.md`](report.md) | All | The assembled final report: executive summary, Controlled Convergence Report (Chair), strengthening plan (Executor), validation (Reviewer). Start here. |
| [`report.html`](report.html) | — | The same report rendered as the styled HTML artifact the skill emits when file output is available. |
| [`appendices/`](appendices) | Council | The six raw, independent advisor reports — Robustness, Maintainability, Operations, Product, Complexity, Cold Onboarder — before any synthesis. This is the "preserved disagreement" the Chair works from. |

## Why this example is worth keeping

- It is a complete trace: divergence (appendices) → convergence (Chair) →
  prepared action (Executor) → verification (Reviewer).
- The Chair preserves three unresolved tensions as explicit human decision
  points (DP1–DP3) rather than collapsing them — the framework's core behavior,
  shown rather than described.
- The findings drove real changes to this repo, so the example and the project
  it reviews stay in sync.

## What happened after this run

This is a verbatim capture, so it reflects the skill *as it was when reviewed* —
several of its findings have since been acted on. Most notably:

- **DP1 (the independence tension) is resolved.** The report left "invest in real
  isolation vs. soften the claim" as a human decision. It was resolved as a
  hybrid: independence is treated as *real* on hosts that can spawn parallel
  subagents or make separate model calls (Claude Code, Codex), and as labeled
  *"distinct-lens"* perspectives in single-session hosts (Claude web, ChatGPT
  chat). See the **Independence requirement** section in `SKILL.md`.
- **Unit A is implemented.** The honest, mode-labeled independence language lives
  in `SKILL.md`, and the Chair groupthink self-check the unit proposed is now in
  both `chairs/systems-architect.md` and `chairs/editor-in-chief.md`.

The example is kept unedited on purpose: it shows the council's real output, and
the repo's later state shows what was done with it.

> Note: this is the curated, annotated copy of the first run, kept under
> `examples/`. The raw outputs of every run (including this one) live under
> `council-reports/`, which is also committed in this repo.
