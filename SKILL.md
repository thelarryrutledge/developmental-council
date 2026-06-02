---
name: developmental-council
description: Run a substantive idea, draft, design, architecture, strategy, or decision through independent advisor stances to surface strengths, risks, hidden assumptions, tensions, and gaps without collapsing to a single verdict. Use when the user asks to council, develop, pressure-test, stress-test, poke holes in, strengthen, or review a real artifact or genuinely uncertain problem. Do not use for simple factual lookup, pure creation, trivial yes/no choices, or low-stakes decisions with no meaningful tradeoff.
---

# Developmental Council

A developmental council strengthens an artifact by preserving multiple perspectives rather than forcing them into one answer. It is useful for generative work: writing, architecture, design, strategy, planning, and important decisions where disagreement is information.

This skill is platform-neutral. Use parallel agents, sub-agents, multiple model calls, or isolated sequential passes depending on what the host platform supports. The important requirement is independence: each advisor must respond without seeing the other advisors' work until the gap pass.

## When to run the council

Run this skill when there is a real artifact or genuinely open problem and the value is in making it stronger.

Good inputs:

- "Council this architecture before I commit to it."
- "Pressure-test this draft. Where does it fail to land?"
- "Develop this strategy with me. What am I missing?"
- "I'm torn between these options and want the tradeoffs surfaced."

Do not run it for:

- Simple factual lookups.
- Pure creation requests where the user wants you to write the thing.
- Trivial naming or implementation choices with little downside.
- Requests where a direct answer, test, benchmark, citation, or calculation is better.

If the user asks for validation but the artifact is substantive, still run the council. A developmental council exists to reveal what the user may be avoiding.

## Core principles

1. **Developmental, not convergent.** The council does not choose a winner, issue a verdict, or merge perspectives into one recommendation.
2. **Report, do not prescribe.** Advisors describe what they see and why it matters. They do not rewrite the artifact or produce replacement text/code unless the user separately asks after the council.
3. **Independent advisor passes.** Advisors must not see one another's responses until the gap pass.
4. **Context isolation.** The Outsider receives only the bare artifact. Other advisors may receive gathered context. Audience context belongs only to the adjudication layer.
5. **No dismissal for comfort.** A valid, in-scope, uncomfortable observation must be flagged up, not quietly marked out of scope.

## Advisor stances

Advisors are thinking stances, not personas. Each seat earns its place by pulling against another seat.

### Contrarian

Assumes the idea has a flaw and goes looking for it. Names what will fail, what is missing, what is being avoided, and where the cost has been underpriced.

Use a domain skin when possible. Examples: on-call maintainer, skeptical buyer, rival tradition expert, honest friend, competitor, regulator, editor.

### First-Principles Thinker

Ignores the surface framing and asks what problem is actually being solved. Strips assumptions, questions the objective function, and identifies when the user may be optimizing the wrong variable.

### Expansionist

Hunts for upside, adjacent opportunity, and underdeveloped strength. Names what is working and what could become larger or more useful if developed.

### Outsider

Receives only the bare artifact with no workspace context, backstory, audience descriptor, or prior discussion. Reacts as someone with fresh eyes. Catches curse-of-knowledge problems, unclear assumptions, missing framing, and places where the artifact only works for insiders.

### Executor

Optional. Use when the artifact implies action, implementation, migration, launch, communication, or follow-through. Focuses on what happens Monday morning, what breaks in practice, and what the smallest credible next step would be.

Drop the Executor for finished-artifact reviews where no action path is relevant.

## Session workflow

### Step 1 — Frame the council brief

Before running advisors, create a neutral brief.

Gather only the context needed to make the review grounded. Depending on the host platform, this may come from attached files, workspace files, repository docs, prior notes, user-provided constraints, or conversation context. Spend little time on context gathering; avoid turning the council into research unless the user asked for research.

Do not give gathered context to the Outsider.

The neutral brief should include:

- The artifact, decision, or problem.
- Key constraints.
- What's at stake.
- Relevant context for non-Outsider advisors.
- Domain and Contrarian skin.
- Whether Executor applies.
- Audience/scope descriptor for adjudication only.

If the input is too vague to frame, ask exactly one clarifying question. If enough is available to proceed, proceed.

### Step 2 — Run independent advisor passes

Use parallel execution if available. If the platform does not support parallelism, run isolated sequential passes and do not expose earlier advisor outputs to later advisors.

Each advisor receives only:

- Its stance.
- The brief, except the Outsider receives the bare artifact only.
- The lean-in instruction.

Advisor prompt template:

```text
You are [Advisor stance] on a developmental council.

Your thinking stance:
[stance description; for Contrarian, include the chosen domain skin]

The artifact brought to the council:
---
[framed artifact; for Outsider, use only the bare artifact]
---

Respond from your stance only. Do not hedge. Do not try to be balanced. Lean fully into your angle; the other advisors cover the angles you do not.

Your job is reporting, not prescribing. Describe what you observe and why it matters. Do not rewrite the artifact, draft replacement text, or produce an improved version. Point to the specific place, assumption, risk, or opportunity and explain its significance. Leave the fix to the author.

[Outsider only: You have no background on the author, domain, goal, audience, or prior context. React only to what is literally in front of you. Do not reconstruct missing context. If you find yourself needing context, flag the absence instead.]

150-300 words. No preamble. Go straight into the analysis.
```

### Step 3 — Gap pass

Collect and anonymize advisor responses as Response A, Response B, etc. Randomize the mapping if possible.

Run one or more independent gap reviewers. The gap reviewers answer only this question:

```text
Several advisors independently examined this artifact:
---
[framed artifact]
---

Their anonymized responses:
[Responses A-E]

One question. Be specific and reference responses by letter, under 150 words:

What did all of these responses miss that the council should consider?

Look especially for connections between responses that no single advisor saw: places where two observations reinforce each other, or where two are in tension in a way that reveals something neither named alone.
```

Do not ask the gap reviewers to rank advisors.

### Step 4 — Optional adjudication layer

Use adjudication when there is enough feedback volume that organization helps. Skip it for short artifacts where the advisor outputs are easy to scan.

The adjudication layer sees:

- The framed artifact.
- All advisor responses.
- Gap-pass outputs.
- The audience/scope descriptor.

It does not produce a verdict, recommendation, rewrite, or merged answer. It organizes the findings so the author can decide what to do.

Adjudication output:

1. **Where advisors converge** — high-confidence signals reached independently.
2. **Where advisors clash** — genuine disagreements, with both sides preserved.
3. **Gaps the council caught** — especially cross-response connections from the gap pass.
4. **Observation adjudication** — sort each observation into exactly one category:
   - **Merit — engage it.** Sound and relevant.
   - **Mistaken — set aside, with reason.** Wrong or based on a false premise.
   - **Out of scope — bracket, with reason.** Valid but not for this artifact, audience, or pass.
5. **Strengthening track** — Expansionist opportunities worth developing vs. scope-creep to skip.

Guardrail: an observation may never be set aside merely because it is uncomfortable, threatening, inconvenient, or audience-challenging. If it is valid and in scope, flag it as uncomfortable but relevant.

### Step 5 — Output

Produce a readable council briefing in the current chat. When the platform supports file output, also create:

- `council-report-[timestamp].html` — scannable report with the framed artifact, convergence, clashes, gaps, adjudication, strengthening track, and collapsible advisor/gap responses.
- `council-transcript-[timestamp].md` — durable transcript with original input, framed artifact, advisor responses, anonymization mapping, gap pass, and adjudication.

If the platform cannot create files, provide the report inline and include the full transcript when requested.

## Context isolation matrix

| Component | Bare artifact | Enriched context | Audience/scope descriptor | Other advisor responses |
|---|---:|---:|---:|---:|
| Contrarian | yes | yes | no | no |
| First-Principles | yes | yes | no | no |
| Expansionist | yes | yes | no | no |
| Executor | yes | yes | no | no |
| Outsider | yes | no | no | no |
| Gap pass | yes | yes | no | yes, anonymized |
| Adjudication | yes | yes | yes | yes, de-anonymized |

## Domain skins for the Contrarian

Choose a skin at framing time. The skin should be structurally opposed to the artifact's likely failure mode, not merely theatrical.

Examples:

- Engineering / architecture: the on-call maintainer who inherits this in six months.
- Strategy / business: the skeptical investor, buyer, competitor, or operator who benefits if this fails.
- Writing / argument: the intelligent reader least inclined to grant the premise.
- Theology / pastoral work: the rival-tradition reader, wounded parishioner, or pastor who must teach this responsibly.
- Design / product: the confused first-time user or stakeholder who must live with the workflow.
- Life decision: the honest friend who suspects the user has already decided.

If no skin fits, run the Contrarian in generic flaw-finding mode.

## Trigger language

Mandatory triggers:

- council this
- develop this
- pressure-test this
- stress-test this
- run the council

Strong triggers when paired with a substantive artifact or open problem:

- what am I missing?
- poke holes in this
- how do I make this stronger?
- review this draft
- review this design
- I am torn between X and Y
- is this the right approach?

## Watch-items

- Contrarian and First-Principles may both say "do not build this" or "the premise is wrong." Keep both if the reasons differ.
- Expansionist can drift into vague encouragement. Force it to name specific strong threads and adjacent opportunities.
- Outsider can accidentally infer context. If it does, tighten the context-starvation instruction.
- Adjudication can rationalize away uncomfortable observations. Apply the guardrail strictly.
- Do not overuse the council. It is intentionally heavier than a normal answer.
