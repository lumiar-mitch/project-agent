---
name: governance-prep
description: Use this to "prep the steering pack", build the board/steerco pack, or prepare ahead of a governance forum. Builds a decision-led pack skeleton per standards/governance-pack.md — leading with the decisions the board must make, then decisions-since, actions arising, top risks, and status claims WITH their evidence. Draft only; the PM owns and presents it.
---

# Governance prep

Build the skeleton of the next governance pack. Governance is **decision-led**: the board exists to
make the calls that cannot be delegated, so the pack leads with those, not with status for its own
sake (`standards/governance-pack.md`, SOUL principle 9). You produce a **draft** — the PM owns it,
edits it, and presents it. You never make or record a decision on their behalf.

## Before you start

1. Read `standards/governance-pack.md`.
2. Identify the forum and its date from PROJECT.md / `wiki/foundation/governance-model.md` (steerco,
   sponsor check-in, board). Note the tolerances that frame what must escalate.
3. Read the last pack in `wiki/governance/` (for "since last forum" continuity) and the current
   `views/` tables and `STATE.md`.

## Assemble the inputs

Pull from the registers:

- **Decisions to be made** — `registers/decisions/` with `status: proposed` or `pending`, plus any
  **tolerance breach** (cost/schedule/scope past the agreed threshold) and any **risk needing formal
  acceptance**. These are the reason the forum meets.
- **Decisions since last forum** — `status: decided` since the previous pack, for noting/ratifying.
- **Actions arising / outstanding** — overdue actions and actions owned by board members.
- **Top-severity risks** — the highest-severity open risks (with owners, responses, review dates).
- **Status claims** — the current RAG picture, each colour paired with its evidence (run
  **status-drift** first so nothing green-without-evidence reaches the board).

## Build the pack skeleton — in this order

Lead with decisions; status comes last.

1. **Decisions required** — for each: the decision, the options considered, the recommendation, and
   what happens if deferred. Draft the framing; leave the recommendation clearly marked as a draft
   for the PM to own or change. This section is the point of the pack.
2. **Tolerance breaches / risks for acceptance** — what has breached, by how much, and the call being
   asked of the board.
3. **Decisions since last forum** — brief log for ratification/awareness.
4. **Actions arising** — overdue and board-owned actions, with owners and dates.
5. **Top risks** — the severe open risks, framed as support requests where relevant.
6. **Status** — RAG per workstream, **each colour with its supporting evidence** (register IDs,
   deliverables, dates). Honest colours only; no watermelons.

## Boundaries

- **Draft only.** You draft the framing, the options, and a marked recommendation. You do not set a
  decision, accept a risk, commit a stakeholder, or finalise a rating — the PM owns the pack and
  presents it.
- Anything leaving the folder (the pack going to the board) needs the PM's explicit approval; you
  prepare, they send.

## Finish

1. File the draft in `wiki/governance/YYYY-MM-DD <Forum> Pack (draft).md`.
2. Append `wiki/log.md`: `## [YYYY-MM-DD] governance | <Forum> pack drafted` with the decisions
   required and the inputs pulled.
3. Report to the PM: the decisions the board must make, anything at a tolerance breach, and any gaps
   you couldn't fill (a decision with no options captured, a status colour with no evidence). Those
   gaps are theirs to close before the pack goes out.
