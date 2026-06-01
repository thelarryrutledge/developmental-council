# Developmental Council

A Claude Code / Cowork skill that runs an idea, draft, design, or decision through several independent advisors — each committed to a distinct thinking stance — then organizes what they found into a briefing you act on, **without collapsing to a single verdict**.

It is built on, and departs from, two prior works (see [Lineage](#lineage)). The departure is the whole point.

---

## Convergent vs. developmental councils

There are two different things you can do with a council of advisors, and they want opposite back ends.

A **convergent council** tests an idea and **produces a verdict**. It's the right design when the problem has a knowable better answer — which product format to ship, which option to pick, what a passage really means. Peer-ranking and a synthesizing chairman serve that goal well. This is what Karpathy and Lehmann built, and for their problems it works.

A **developmental council** — this skill — **strengthens an artifact** by surfacing distinct perspectives and the tensions between them, then **stops**, leaving the synthesis to you. It's the right design for generative work — writing, architecture, design, strategy — where collapsing five perspectives into one verdict destroys the value, because the disagreements and the gaps *are* the product.

Same spawn-and-collect machinery. Opposite objective function. This repo is not an improvement on the convergent council; it's a **different tool that shares its lineage**, aimed at a different class of problem.

---

## What it does

1. **Frames** your artifact neutrally and scans the workspace for grounding context (withholding that context from the Outsider seat — see below).
2. **Convenes** five advisor stances in parallel, each told to lean fully into its angle and to *report what it sees, not rewrite your work*:
   - **Contrarian** (takes a per-domain skin) — what will fail, what you're avoiding.
   - **First-Principles** — are you even solving the right problem?
   - **Expansionist** — upside and adjacent opportunity; what's strong and worth developing.
   - **Outsider** — reacts with zero context; catches the curse of knowledge.
   - **Executor** (optional per run) — what actually happens Monday morning.
3. **Runs a gap pass** — anonymized advisors answer one question: *what did everyone miss?*, with emphasis on connections between responses no single advisor saw.
4. **Adjudicates** (optional) — organizes everything into converge / clash / gaps, sorts each observation into *merit / mistaken / out-of-scope*, and keeps a separate *strengthening* track. It never merges, ranks, or issues a verdict.
5. **Outputs** a scannable HTML report and a full markdown transcript.

---

## Install

1. Download `SKILL.md` from this repo.
2. In Claude Code or Cowork: **Customize → Skills → Add skill**, and paste the name and description separately, then the body.
3. Trigger with `council this`, `develop this`, `pressure-test this`, etc., followed by your artifact and as much context as you can give it.

Optional: run the adjudication layer only when feedback volume warrants it (it's the last, skippable step).

---

## Lineage

- **Andrej Karpathy — LLM Council** (Nov 2025). The original: dispatch a query to multiple models (via OpenRouter), have them peer-review each other anonymously, and a chairman model synthesizes the final answer. Multi-model by design. <https://github.com/karpathy/llm-council>
- **Ole Lehmann — LLM Council skill for Claude** (early 2026). Rebuilt the council to run entirely inside Claude using sub-agents with distinct *thinking styles* instead of different models, with a five-advisor lineup (Contrarian, First-Principles, Expansionist, Outsider, Executor), anonymized peer review, a chairman verdict, and an HTML report. Article: <https://x.com/itsolelehmann/status/2038661433626333649>

Credit for the advisor-as-thinking-stance design, the lean-in instruction, the trigger taxonomy, the workspace context scan, and the two-file output goes to Lehmann; credit for the dispatch / anonymous-review / chairman structure goes to Karpathy. Their convergent design is the *right* design for their problems — this skill keeps most of their machinery and changes only what a developmental aim requires.

---

## What we changed, and why

| Change | Why |
|---|---|
| **Removed the peer-review ranking** ("which response is strongest / has the biggest blind spot"); kept only "what did everyone miss?" | A single underlying model evaluating its own outputs exhibits self-preference bias even when responses are anonymized — anonymization hides the label, not the style the model recognizes as its own. The "what did everyone miss" question, and especially cross-response connections, carries the developmental value without the biased ranking. (See *LLM Evaluators Recognize and Favor Their Own Generations*, NeurIPS 2024, arXiv:2404.13076.) |
| **Replaced the verdict-chairman with an adjudication layer.** Kept Lehmann's *converge / clash / blind-spots* sections; removed *the recommendation* and *the one verdict*. | Those first three sections are already developmental — they surface perspectives and keep tensions visible. The verdict collapses them. For generative work the conflicts and gaps are the product; resolving them is the author's job, not the council's. |
| **Added a no-dismiss-for-comfort guardrail** to the adjudication layer. | An audience-aware layer can quietly reclassify valid, in-scope, *uncomfortable* observations as "out of scope." The guardrail permits setting an observation aside only for being *mistaken* or *out-of-scope*, never for being *threatening*, and forces uncomfortable-but-relevant items to be flagged up. |
| **Context-isolated the Outsider seat.** | A concrete fix to a real bug in the convergent Claude skill: its workspace-context scan feeds enriched context to *every* advisor, including the Outsider — silently contaminating the one seat whose entire value is reacting *without* context. Here the Outsider explicitly receives only the bare artifact. |
| **Advisors stay audience-blind; only the adjudication layer knows the audience.** | If audience context leaks into an advisor, it self-censors the objections it assumes the audience won't care about — the exact contamination separate agents exist to prevent. |
| **Report-don't-prescribe + no-rewriting rule** on every advisor. | The council produces *information about the artifact*, never a replacement draft. This keeps authorship — and the synthesis — with the user. |
| **Domain skins for the Contrarian; per-run audience descriptor.** | Generalizes a single-domain tool to any topic via structural (not role-played) opposition, while the audience is supplied per run instead of hardcoded. |
| **Made the adjudication layer optional/skippable.** | On short artifacts it's overhead between author and work; it earns its cost only when feedback volume is high. |

A note in fairness: none of these are corrections of mistakes in the convergent councils except the Outsider-isolation bug. The rest are consequences of pointing the same machinery at a different problem.

---

## License

MIT — see [LICENSE](LICENSE).
