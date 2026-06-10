# Advisor Appendix — Operations

## Advisor
Operations Advisor

## Focus
Observability, run repeatability, cost steerability, and output-fallback behavior.

## Design-Health Score
58 — Metadata infrastructure is partially implemented but incomplete; execution_mode is self-reported without verification; multi-run analysis is half-finished; partial-output fallback is undefined.

## Key Findings
1. **High — YAML metadata block is inconsistently applied.** Historical runs vary (an earlier run lacks the block entirely; a later one has it). Without 100% compliance, cross-run analysis is unreliable. *(Note: the earliest run predates the metadata requirement.)*
2. **High — Metadata lacks a machine-actionable outcome/status field.** It records scope/mode/count/advisors/date/package but nothing about success, phase reached, verification result, or token cost — so dashboards can't answer "how many passed?" or "average cost?"
3. **High — execution_mode is self-reported with no verification checkpoint.** A single-session run could falsely claim multi-agent and be indistinguishable.
4. **Med — File-naming spec-vs-reality mismatch.** Spec says `counterpoint-report-[timestamp].md`; reality is a fixed name inside a `[timestamp]/` dir. Reversible, but a pattern problem for programmatic queries.
5. **Med — Partial-output fallback is documented but not actionable.** "Fall back to chat-only when unavailable" doesn't define what counts as unavailable, whether to write markdown-only, or how to record the degradation.

## Major Concerns
1. Cost predictability is aspirational: "advisor count is the lever" but no way to know cost in advance.
2. Run-id stability is weak (human timestamps, possible collisions, no stable key).
3. Traceability completeness varies across historical runs; cross-run analysis will be mixed.
4. Output directory implies ceremony but has no manifest/validation that all files are present.
5. Reduced-advisor steering is declared but mechanically unimplemented (no syntax/parsing/validation).

## Recommendations
1. Make the metadata block mandatory and validate it at assembly time (fail the build if malformed).
2. Add `outcome`, `phases_completed`, and an approximate `token_estimate_in` to the block.
3. Add an execution_mode assertion/verification in Phase 1; auto-downgrade to single-session if parallelism isn't real.
4. Use a stable, sortable file name (timestamp in the filename), not nested dir + fixed name.
5. Define the partial-output fallback explicitly (`html_generated: false`, etc.; escalate on write failure).

## Must-Preserve Elements
- The YAML frontmatter concept; the "From advisors/From synthesis" distinction; execution_mode as an independence-calibration frame (fix verification, don't remove); the opt-in four-phase structure; appendix-based advisor reports.

## Confidence
High — the metadata gaps are observable in existing runs, not predicted.

## Notes for the Chair
The metadata investment is ~80% done; the last 20% (outcome/cost fields, execution-mode verification, reduced-advisor syntax) is the load-bearing part for multi-run analysis. execution_mode has become a *trust field* central to the independence claim, so it should not stay purely self-reported. All additions are reversible and low-cost; deferring them makes future analysis fragile.
