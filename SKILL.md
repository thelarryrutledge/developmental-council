---
name: developmental-council
description: "Run any idea, draft, design, or decision through a council of independent advisors who each analyze it from a distinct thinking stance, surface where they agree and clash, and hand you an organized briefing — WITHOUT collapsing to a single verdict. This is a DEVELOPMENTAL council (it strengthens an artifact by surfacing perspectives and their tensions), as distinct from a CONVERGENT council (which tests a decision and produces one answer). MANDATORY TRIGGERS: 'council this', 'develop this', 'pressure-test this', 'stress-test this', 'run the council'. STRONG TRIGGERS (use when paired with a real artifact or open problem): 'what am I missing', 'poke holes in this', 'how do I make this stronger', 'review this design', 'review this draft', 'I'm torn between X and Y', 'is this the right approach'. Do NOT trigger on simple factual lookups, trivial yes/no questions, pure creation requests ('write me X'), or low-stakes 'should I' questions with no real tradeoff. DO trigger when the user brings a substantive artifact or genuinely uncertain problem they want examined from multiple angles."
---

# Developmental Council

You bring one idea to one model, you get one perspective — shaped by how you framed it. This council runs your idea, draft, design, or decision through several independent advisors, each committed to a distinct thinking stance, then organizes what they found into a briefing you act on.

It is deliberately a **developmental** council, not a **convergent** one. That distinction is the entire point and governs every design choice below.

- A **convergent council** (Karpathy's original LLM Council; Lehmann's Claude adaptation) tests an idea and **produces a verdict**. It is optimized for decisions that have a knowable better answer — which option to pick, which product format to ship. Peer-ranking and a synthesizing chairman serve that goal well.
- A **developmental council** (this skill) **strengthens an artifact** by surfacing distinct perspectives and the tensions between them, and then **stops** — leaving the synthesis to you. It is optimized for generative work (writing, architecture, design, strategy) where collapsing to a single verdict destroys the value, because the disagreements and gaps *are* the product.

Same spawn-and-collect machinery as its predecessors. Opposite back end. See README for full lineage and attribution.

---

## When to run the council

Run it when there is a real artifact or a genuinely open problem and the value is in *making it stronger*, not in *picking a winner*.

Good developmental-council inputs:
- "Here's my architecture for X — what's wrong with it, what's it missing, where will it hurt in six months?"
- "Here's a draft. Where does it fail to land, what's it assuming, where's it drifting?"
- "I'm designing this API. Pressure-test the shape before I commit."
- "I keep going back and forth on this approach. Develop it with me."

Bad inputs (don't council these):
- Factual lookups ("what's the syntax for X") — just answer.
- Pure creation ("write me a function / a tweet") — that's a task, not a development pass.
- Trivial decisions with no real tradeoff ("should I name this `count` or `total`") — overhead, not insight.

If you already know the answer and want validation, skip it. A developmental council exists to tell you what you'd rather not hear about your own idea.

---

## The advisors (stances, not roles)

Advisors are **thinking stances**, not job titles or personas. They are defined by *how* they think, which makes them portable across any domain. The core five form three productive tensions — and a seat earns its place by being **in tension with another seat**. If a proposed advisor has no opposing advisor, it is not pulling weight; cut it.

The three tensions:
- **Contrarian ↔ Expansionist** — downside vs. upside.
- **First-Principles ↔ Executor** — rethink the whole thing vs. just ship it.
- **Outsider** sits in the middle, holding everyone honest with fresh eyes.

### 1. The Contrarian
Assumes the idea has a flaw and goes looking for it — what will fail, what's missing, what you're avoiding. Not a pessimist; the friend who saves you from a bad call by asking the question you're dodging.
**This is the one seat that takes a per-domain SKIN** (see Domain Skins below), because the strongest opposition is domain-specific: a rival-tradition expert, an on-call engineer who'll maintain this at 3am, a skeptical buyer, etc.

### 2. The First-Principles Thinker
Ignores the surface question and asks what you're *actually* trying to solve. Strips assumptions, rebuilds from the ground up. Its highest-value output is often "you're optimizing the wrong variable entirely."

### 3. The Expansionist
Hunts for upside everyone else misses. What could be bigger, what adjacent opportunity is sitting right next to this, what's being undervalued. Doesn't care about risk (that's the Contrarian's job) — cares about what happens if this works better than expected. This is the **generative / coach** seat: it also names what's *strong* and should be developed further.

### 4. The Outsider
Has **zero context** about you, your field, your history, or your goal. Responds purely to what's in front of it. Catches the curse of knowledge — what's obvious to you but invisible to everyone else.
**CRITICAL: this seat must be context-starved.** See "Context isolation" — getting this wrong silently defeats the most valuable advisor.

### 5. The Executor
Cares about one thing: can this actually be done, and what's the fastest real path? Ignores theory. Looks at every idea through "OK, but what do you do Monday morning / what breaks in practice?" Flags brilliant plans with no first step.
**This seat is optional per preset** — drop it for finished-artifact reviews (e.g. a polished essay) where there's no "next action," keep it for designs and decisions.

---

## How a session works

### Step 1 — Frame the question (with context enrichment)

When triggered, do two things before spawning advisors:

**A. Scan the workspace for context** — but **NOT for the Outsider.** Quickly glob/read the 2-3 files that would let advisors give grounded, specific feedback instead of generic takes:
- `CLAUDE.md` / project context files
- any `memory/` or notes folder
- files the user referenced or attached
- recent council transcripts in this folder (avoid re-counciling the same ground)
- domain-relevant data (for an architecture question, the relevant code/configs; for a strategy question, the relevant numbers)

Spend ~30s max. **The context you gather here is passed to Contrarian, First-Principles, Expansionist, and Executor — and is deliberately WITHHELD from the Outsider.** The Outsider receives only the bare artifact. This is not an oversight to "fix" — the Outsider's entire value is reacting without your context.

**B. Frame the artifact neutrally.** Reframe the user's input + enriched context into one clear, non-steering brief all advisors (except the context-starved Outsider) receive. Include: the artifact/decision itself, key context, constraints, and what's at stake. Do not inject your own opinion. If the input is too vague to frame, ask exactly **one** clarifying question, then proceed.

Also determine, at framing time:
- the **domain** (drives the Contrarian's skin — see below)
- whether the **Executor** seat applies for this input
- the **audience/scope descriptor** for the adjudication layer (who this is for, what counts as in-scope). This is passed ONLY to the adjudication layer, never to the advisors.

### Step 2 — Convene the advisors (parallel)

Spawn all applicable advisors **simultaneously** as sub-agents (sequential spawning lets earlier responses bleed into later ones and breaks independence). Each receives: its stance, the framed artifact (Outsider: bare artifact only), and the **lean-in instruction** below.

**Advisor prompt template:**
```
You are [Advisor stance] on a developmental council.
Your thinking stance: [stance description above; for the Contrarian, include the domain skin]

The artifact brought to the council:
---
[framed artifact — for the Outsider, the BARE artifact with no enrichment]
---

Respond from your stance only. Do NOT hedge. Do NOT try to be balanced.
Lean fully into your angle — the other advisors cover the angles you don't.
Your job is REPORTING, not prescribing: describe what you observe and why it
matters. Do NOT rewrite the artifact, draft replacement text, or produce an
"improved version." Point to the specific place and explain the issue or the
opportunity; leave the fix to the author.

[Outsider only: You have NO background on the author, the field, or the goal.
React only to what is literally in front of you. Do not try to reconstruct the
missing context — if you find yourself inferring it, flag that instead of inferring.]

150-300 words. No preamble. Go straight into your analysis.
```

The **report-don't-prescribe** rule and the **no-rewriting** rule are load-bearing: this council produces *information about the artifact*, never a new draft of it. Models default to "helpfully" suggesting edits — suppress that in every advisor.

### Step 3 — The gap pass (parallel)

This is the developmental analogue of peer review. **We deliberately do NOT rank the advisors** (no "which response is strongest"). Single-model self-evaluation favors its own generations regardless of anonymization (see README — NeurIPS 2024 self-preference finding), so ranking is biased noise. We keep only the genuinely valuable question.

Collect all advisor responses, anonymize as Response A…E (randomize the letter mapping). Spawn one reviewer per advisor; each sees all anonymized responses and answers a **single** question:

**Gap-pass prompt template:**
```
Several advisors independently examined this artifact:
---
[framed artifact]
---
Their anonymized responses:
**Response A:** [response]
... (B–E) ...

One question. Be specific, reference responses by letter, under 150 words:
What did ALL of these responses MISS that the council should consider?
Look especially for connections BETWEEN responses that no single advisor saw —
where two observations reinforce each other, or where two are in tension in a
way that reveals something neither named alone.
```

The cross-response connection prompt is where the highest-value insights come from — a relationship between two advisors' points that neither saw alone.

### Step 4 — Adjudication layer (NOT a verdict-chairman)

One agent receives: the framed artifact, all advisor responses (now de-anonymized), all gap-pass outputs, and the **audience/scope descriptor**. It is the **only** component that knows the audience.

It does NOT merge the advisors into one answer, does NOT rank them, does NOT rewrite the artifact, and does NOT produce a single recommended verdict. It **organizes and adjudicates** so the author can act efficiently, leaving conflicts standing.

**Adjudication output structure:**

1. **Where the advisors converge** — points multiple advisors reached independently. High-confidence signals.
2. **Where the advisors clash** — genuine disagreements. Present both sides, explain why each is reasonable. **Do not resolve these** — the tension is information the author needs; resolving it is the author's job.
3. **Gaps the council caught** — what emerged only from the gap pass, especially cross-response connections.
4. **Adjudication of each observation** — sort every advisor observation into exactly one of:
   - **Merit — engage it.** Sound and relevant to this artifact/audience.
   - **Mistaken — set aside, with reason.** The observation is wrong (e.g. attacks a premise/constraint that doesn't actually apply).
   - **Out of scope — bracket, with reason.** Valid, but not for this artifact, audience, or pass.
5. **Strengthening track (Expansionist)** — handled separately from objections: which strengthening moves are worth the effort/scope, which are scope-creep to skip. You *act on* these, you don't *defend against* them.

**THE GUARDRAIL (non-negotiable):** An observation may be set aside ONLY for being *mistaken* or *out of scope*. It may **NEVER** be set aside for being *threatening* — i.e. valid, in-scope, and merely uncomfortable for the author or audience. If an observation is valid and in-scope but the temptation is to drop it for comfort, **flag it UP** as high-priority "uncomfortable but relevant." Distinguishing "doesn't affect my audience" (legitimate scope call) from "would challenge my audience in a way I'm avoiding" (threat-avoidance) is the layer's single most important function. Scope is editorial judgment; threat-avoidance is how the work gets worse.

The adjudication layer produces **no prose for the artifact** — only the briefing the author uses to decide where to spend the next pass.

**Optionality:** The adjudication layer is the last step and should be skippable. On short artifacts, the advisor outputs are sortable by eye and the layer just inserts overhead between author and work. Invoke it when the volume of feedback warrants it. (Recommend opt-in via a flag.)

### Step 5 — Output: report + transcript

Produce two files in the workspace:

`council-report-[timestamp].html` — a single self-contained HTML file (inline CSS, system-font stack, clean professional-briefing look). Contents:
- the framed artifact at top
- the adjudication briefing prominently (converge / clash / gaps / adjudication / strengthening)
- a simple **convergence-and-tension visual** — show which advisors aligned and which diverged (a grid or spectrum). It must visualize *tension*, not a ranking or a winner.
- collapsible full advisor responses (collapsed by default)
- collapsible gap-pass section
- footer: timestamp + what was counciled

Open the file after generating.

`council-transcript-[timestamp].md` — full transcript: original input, framed artifact, all advisor responses, all gap-pass outputs (with the anonymization mapping revealed), the adjudication briefing. This is the durable artifact: re-counciling the same input later, the prior transcript shows how the thinking evolved.

---

## Domain skins (the Contrarian seat)

Only the Contrarian takes a domain skin, chosen at framing time from the domain. The skin commits the seat to a *real, specific* opposing position rather than generic doubt — structural independence, not role-play. Examples:

- **Engineering / architecture** → the on-call maintainer who inherits this in six months and will be paged for it; argues operational reality, hidden coupling, simpler shapes.
- **Strategy / business decision** → the skeptical investor or the competitor who benefits if you're wrong.
- **General life decision** → the honest friend who suspects you've already decided and are seeking permission.
- **(Writing/theology and other specialized domains)** → defined in a separate, domain-specific preset, not shipped here.

If no skin fits cleanly, the Contrarian runs in its generic flaw-finding mode.

---

## Context isolation matrix (get this exactly right)

| Advisor | Artifact | Enriched workspace context | Audience descriptor |
|---|---|---|---|
| Contrarian (skinned) | ✅ | ✅ | ❌ |
| First-Principles | ✅ | ✅ | ❌ |
| Expansionist | ✅ | ✅ | ❌ |
| Executor (optional) | ✅ | ✅ | ❌ |
| **Outsider** | ✅ (bare) | **❌ — must be clean** | ❌ |
| Adjudication layer | sees all outputs | ✅ | ✅ (only component that knows audience) |

Two rules that are easy to break and silently ruin the council:
1. **The Outsider gets a genuinely bare context.** If your framework defaults to passing workspace/enrichment to every sub-agent, the Outsider is contaminated and you won't notice. Spawn it explicitly clean.
2. **The advisors stay audience-blind.** Only the adjudication layer knows the audience. If audience context leaks into an advisor, it self-censors the objections it assumes the audience won't care about — exactly the contamination separate agents exist to prevent.

---

## Important notes

- **Spawn advisors in parallel**, never sequentially.
- **Report, don't prescribe** — advisors describe what they see; they never rewrite the artifact.
- **No ranking, no verdict, no merging** — the council organizes perspectives; the author synthesizes. The conflicts and gaps are the product.
- **The guardrail holds** — set observations aside only for being mistaken or out-of-scope, never for being uncomfortable.
- **Cost awareness** — a full run is roughly (advisors + gap-pass + adjudication)× a single query. It's a deliberately-invoked tool for substantive artifacts, not a reflex on everything. Run it as a reflex and you'll start producing work *for* the council.

---

## Watch-items (verify on real runs, not in design)

- **Contrarian vs. Expansionist overlap** — different axes (downside vs. upside) but may land on the same spot. If the Expansionist is just softening the Contrarian, re-scope it toward genuine adjacent-opportunity rather than reassurance.
- **Expansionist drifting into flattery/vagueness** — its failure mode is bland encouragement. If outputs read as "nice, add more," tighten the "name the specific strong thread and how to develop it" instruction.
- **Adjudication layer rationalizing** — watch for valid-but-uncomfortable observations quietly classified "out of scope." If a set-aside's stated reason doesn't survive the mistaken-vs-threatening test, the guardrail isn't holding.
- **Outsider reconstructing context** — if its output shows it inferred the field/goal from the artifact, its context isn't clean enough or the resist-inference instruction is too weak.
