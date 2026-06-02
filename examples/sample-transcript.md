# Sample Council Transcript (illustrative)

> **This is a hand-constructed illustration, not a live run.** It shows the *shape* of
> the council's output — distinct stances, a gap pass, and a non-collapsing adjudication —
> on a deliberately neutral toy artifact, so a reader can see the expected format without
> any real project being referenced. For proof that the skill actually *executes* (real
> sub-agents spawned in parallel, real gap-pass convergence), see
> [`sample-run-real.md`](sample-run-real.md), which is the verbatim output of a live run.

The toy artifact below contains intentional weaknesses for the council to find. No real
project is referenced.

---

## Original input

> council this: I want to add a feature to my note-taking app where every note the
> user writes is automatically posted to a public feed by default, so people can
> discover each other's notes. Users can toggle a note to private if they want.

## Framed artifact

A note-taking app proposes making all notes **public by default**, posted to a shared
discovery feed at creation time, with an opt-out toggle to mark a note private.
Goal: drive discovery and cross-user engagement. At stake: user trust, the product's
core "place to think" value, and potential exposure of unintended content.
*(Context starved for the Outsider; full framing for the rest.)*

---

## Advisor responses

**The Contrarian (skin: the privacy-minded user who'll be burned by this).**
Public-by-default with opt-out is the single most predictable way to leak private
content. The failure mode isn't hypothetical: a user jots a password reminder, a
half-formed rant about their boss, a medical note — and it's public the instant they
save, before they think to toggle. Opt-out puts the burden of caution on the user at
exactly the moment they're least focused on it. Every product that has tried
public-by-default for personal content has paid for it in trust. The toggle doesn't
save you; it just gives you someone to blame.

**The First-Principles Thinker.**
What are you actually trying to solve — discovery, or engagement? Those are different
problems. If the real goal is "users find this app lonely," the answer might be
templates, prompts, or import tools, not exposing private writing. You've assumed the
unit of sharing is *the note*, but a note-taking app's notes are mostly not meant for
anyone. The premise — that notes are latent public content — may be the actual error.
A "place to think" and "a social feed" are arguably opposite products.

**The Expansionist.**
There's a real opportunity adjacent to this, but it's the inverse of the proposal:
opt-*in* sharing of *curated* notes could become a genuine feature — a "publish"
action that turns a private note into a shareable page. That's the strong thread:
discovery built on deliberate publishing, not ambient exposure. Done that way, it
could anchor a whole creator surface (public profiles, collections) without touching
the trust of the private core. The instinct to enable discovery is good; the default
is what's backwards.

**The Outsider (no context).**
I don't know this app. Reading only the description: "everything you write is public
unless you remember to hide it" is the part that stops me. I wouldn't write anything
honest in a tool that works that way, and I wouldn't know, while typing, whether what
I'm writing is about to be seen. If the goal is people sharing, I'd expect a button
that says "share this," not a switch I have to find and flip the other way.

**The Executor.**
What ships Monday? Not this — public-by-default is a one-way trust door and a likely
incident. The cheapest real test of the actual goal: add a single "Publish" button to
existing notes, route published notes to a simple feed, measure whether anyone uses it.
Two days of work, reversible, no default changed, no exposure risk. If publishing gets
no usage, the discovery hypothesis was wrong and you saved yourself the blast radius.

---

## Gap pass (anonymized; "what did everyone miss?")

The reviewers converged on one thing no single advisor stated outright: **the proposal
and its strongest alternative differ by exactly one word — default.** Three advisors
(Expansionist, Outsider, Executor) independently described the *same fix* (an opt-in
"publish" action) from three directions — opportunity, comprehension, and shippability —
without any of them naming that their agreement is the signal. The convergence of an
upside-seat, a fresh-eyes seat, and a pragmatics-seat on the identical design move is
the strongest evidence in the room. Separately: every advisor treated this as a privacy
question; none asked whether a public feed of others' notes is even *desirable to read* —
the demand side of "discovery" went unexamined.

---

## Adjudication briefing

**Where the advisors converge.** Public-by-default is the wrong default (4 of 5,
independently). Opt-in publishing of curated notes is the safer and likely stronger
design (3 of 5, from different angles — the gap pass flagged this convergence as the
high-confidence signal).

**Where the advisors clash.** Whether discovery is the right goal *at all*:
First-Principles questions the entire premise (a thinking tool and a social feed may be
opposite products); the Expansionist sees a real creator-surface opportunity. This is a
genuine product-strategy fork — **left standing for the author.** It is not the
council's to resolve.

**Gaps the council caught.** The demand side of discovery (is a feed of strangers'
notes worth reading?) went unexamined by every seat. Worth investigating before
building either version.

**Adjudication of observations.**
- *Merit — engage:* the leak risk of opt-out (Contrarian); the opt-in "Publish"
  reframe (Expansionist/Outsider/Executor); the cheap reversible test (Executor).
- *Mistaken — set aside:* none. No advisor argued from a false premise.
- *Out of scope — bracket:* the full creator-surface vision (profiles, collections) is
  valid but beyond a first feature; revisit if publishing shows demand.

**Strengthening track (Expansionist).** The "Publish" action is worth building; the
broader creator surface is scope-creep for now — bracket it.

> No uncomfortable-but-relevant items were suppressed. The hardest observation (the
> Contrarian's "the toggle just gives you someone to blame") is carried in full under
> Merit, not softened.

**No verdict issued.** The author decides whether to pursue discovery at all, and if so,
which version — the council has organized the perspectives and kept the strategy fork open.

---

*Generated as a behavior demonstration on a toy artifact. A real run also produces a
`council-report-[timestamp].html` alongside this transcript.*
