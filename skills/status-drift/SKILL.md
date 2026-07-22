---
name: status-drift
description: Use this for a "status check", whenever a status report is ingested, or when called by weekly-review. The de-watermeloner — compares status claims against register evidence and prior periods (per standards/rag-evidence.md) to catch green/amber with no evidence, slippage behind green, severe open risks under "on track", and estimates that never move. Frames red as a request for support.
---

# Status drift

Catch the gap between what the status *says* and what the evidence *shows*. Every RAG colour is a
claim; your job is to test it against the registers and the prior periods, per
`standards/rag-evidence.md`. You report the drift — you do not re-colour the status; the RAG rating
is the human's to own.

## Before you start

1. Read `standards/rag-evidence.md`.
2. Gather the **current** status claims — from the status report just ingested, or the latest status
   in `wiki/` / STATE.md.
3. Gather the **evidence base**: `views/raid.md`, `registers/risks/`, `registers/actions/`,
   `registers/decisions/`, milestones/dates in PROJECT.md.
4. Gather the **prior periods**: the previous status report(s) for the same workstream, so you can
   test movement.

## Drift tests

For each reported colour (overall and per workstream), run these checks:

1. **Colour with no observable evidence.** A green or amber with nothing behind it — no completed
   deliverable, no measured data. Flag as *unverified*.
2. **Slippage behind green.** A milestone date that has moved later while the colour stayed green,
   or a date that will be missed on current run-rate.
3. **Severe open risks under "on track".** Open risks with high severity, or overdue actions, sitting
   under a green/on-track claim. The status is greener than the RAID.
4. **Estimates that never move.** "90% done" across three periods; a completion date that is always
   "two weeks away"; effort/cost estimates frozen while the work isn't. Stalled estimates are a
   watermelon smell.
5. **Colour vs prior period.** A jump green→red with no intervening amber, or a persistent green
   through a period where risks materialised — inconsistency that needs explaining.

## Output

For each colour, present:

- The **claim** (colour + who/what it covers).
- The **supporting evidence** (register IDs, completed deliverables, dates) — or "none found".
- The **contradicting evidence** (overdue actions, slipped dates, open severe risks), with IDs and
  absolute-dated citations.
- Your **read**: verified / unverified / contradicted.

Where the evidence says the true colour is worse than reported, say so plainly — never soften bad
news to keep a dashboard green. **Frame red as a request for support**, not a confession: name what
help or decision would move it.

## Boundaries and handoff

- You surface the drift and propose the honest colour; **you do not change the RAG rating** — that
  is the PM's to set and to present.
- When called by **weekly-review**, return your findings as the watermelon-hunt section (don't file
  separately).
- When run standalone: append `wiki/log.md`:
  `## [YYYY-MM-DD] review | Status drift check` with the colours tested and the drift found; if the
  check produced real synthesis, offer to file it in `wiki/answers/`.
