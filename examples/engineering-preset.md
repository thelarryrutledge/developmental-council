# Preset: Engineering / Architecture Review

A worked configuration of the developmental council for technical design work —
architecture decisions, API shapes, infrastructure choices, refactors. Drop this
context into the framing step, or keep it as a reference for how to skin the council
for engineering.

## When to use
Bring a design, not a bug. The council develops *decisions with no single right
answer* — "S3 vs. Postgres for state," "is this abstraction earning its keep,"
"will this coupling hurt in six months." It is **not** for questions with a knowable
answer (use a test, a benchmark, or a straight answer for those).

## Seat configuration

- **Contrarian — skin: the on-call maintainer who inherits this in six months.**
  Argues operational reality: what pages someone at 3am, hidden coupling, the failure
  mode no one designed for, the simpler shape that would have avoided this. Not
  "is the code wrong" — "what will this cost to live with."
- **First-Principles** — "what are we actually solving?" Catches the wrong-variable
  trap: optimizing throughput when the real constraint is operability; building a
  framework when a script would do; solving a problem the architecture shouldn't have
  created in the first place.
- **Expansionist** — adjacent leverage. Does this design unlock something bigger
  (a reusable primitive, a capability the team's been wanting)? What's the strong part
  worth investing further in?
- **Outsider** — context-starved. Reads the design with no knowledge of the system,
  the team's history, or the constraints. Catches what's only obvious to people who
  already hold the system in their heads — the onboarding cliff, the implicit
  assumption, the undocumented "everyone knows that."
- **Executor — KEEP for engineering.** What's the smallest first step? Can this ship
  incrementally or is it a big-bang rewrite? What's the migration path? Flags
  designs that are elegant on paper with no realistic path to production.

## Domain context to gather (Step 1A) — but NOT for the Outsider
- The relevant code / configs / manifests for the component in question.
- `CLAUDE.md` or architecture docs describing the system and its constraints.
- Past decisions / ADRs (and prior council transcripts) on adjacent choices.
- Operational reality: what's currently on-call burden, what's already fragile.

## Audience / scope descriptor (adjudication layer only)
Typically: "the team that maintains this; we value explicit, operable,
self-hostable infrastructure over managed-service convenience; this is a
[reversible / one-way-door] decision." Adjust per decision — the
reversible-vs-irreversible framing strongly affects what counts as in-scope.

## Tension-pairs in this domain
- Contrarian (operability cost) ↔ Expansionist (capability upside)
- First-Principles (don't build this) ↔ Executor (here's how to ship it)
- Outsider holds the middle: "I don't understand why this exists."

## Watch-item specific to engineering
Contrarian and First-Principles will often *both* say "don't build this" — one on
operability grounds, one on wrong-problem grounds. That's not redundancy if the
*reasons* differ; the adjudication layer should keep both and note whether they
reinforce (strong signal to stop) or diverge (two separate problems).
