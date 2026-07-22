---
name: project-interview
description: Use this when the project has no charter, PROJECT.md is empty or thin, or the user wants to (re)establish the project particulars — "set up this project", "let's do the interview", "capture the project basics". Runs a staged interview that seeds PROJECT.md and the registers without ever blocking on a missing answer.
---

# Project interview

Establish the project's particulars through a short, staged conversation. You are gathering
facts, not designing the project — capture what the human tells you, confirm before you write,
and park anything they cannot yet answer. Never invent a fact and never set a field the human
has not confirmed.

## Before you start

1. Read `PROJECT.md`, `STATE.md`, and `wiki/index.md` if they exist. If PROJECT.md already
   holds particulars, treat this as a top-up: only ask about the gaps and the "Open particulars".
2. Read `SOUL.md` so your voice matches (direct, plain, Australian English).
3. Tell the human what this is: four short blocks of questions, roughly 10–15 minutes, and that
   they can say "skip", "don't know yet", or "later" to anything — it goes to a parking list, it
   never stops the interview.
4. Ask the blocks **one at a time**. Where a block has several factual fields, use the structured
   question tool to gather them together rather than a prose interrogation. Read back what you
   heard before writing anything.

## Block 1 — Identity & intent

Purpose: what this project is and why it exists. Ask:

- Project name (and any code/short name).
- One-sentence purpose / the outcome it must deliver.
- The business case or driver — why now, what problem it solves.
- Current phase / stage (initiating, planning, delivery, closing).
- Sponsor (named person) and the delivering organisation(s).

Write these into `PROJECT.md` under **Identity**. If a charter or business-case document exists,
note its path; if the human mentions one that isn't filed yet, add "charter document" to Open
particulars and offer to ingest it.

## Block 2 — Scope

Purpose: the boundary. Ask:

- In scope — the main deliverables or workstreams.
- Explicitly out of scope — what people might assume is included but isn't.
- Key milestones and target dates (get real dates; "mid-year" → ask for a month).
- Known constraints — time, cost, scope, resource, regulatory, technical.

Write the scope narrative into `PROJECT.md` under **Scope** (and it seeds
`wiki/foundation/scope.md` later during ingest). For each firm constraint, **seed a constraint
register item** `registers/constraints/CON-### Title.md` with `title, statement, category(time|cost|scope|resource|regulatory|technical),
authority, negotiable, implications`. Read the constraint back before filing.

## Block 3 — Governance & people

Purpose: who decides and who cares. Ask:

- Governance forums — steering committee / board / sponsor check-ins, their cadence, and the
  next date.
- Delivery tolerances — what the PM can decide vs what must escalate (cost/schedule/scope
  thresholds), if known.
- Key stakeholders — name, role, organisation, and a first read on influence and interest.
- The delivery team and key roles.

Write governance and tolerances into `PROJECT.md` under **Governance** (seeds
`wiki/foundation/governance-model.md`). Write the team into **Team** (seeds
`wiki/foundation/team.md`). For each named stakeholder, **seed a stakeholder register item**
`registers/stakeholders/STK-### Name.md` with `name, role, org, category, influence(1–5),
interest(1–5), sentiment, sentiment_assessed(today), engagement, comms_cadence, key_concerns`.
You may record influence/interest as the human's first read; leave `sentiment` at neutral unless
they state one — sentiment is the human's assessment to give, not yours to guess.

## Block 4 — Hard facts

Purpose: the load-bearing numbers and dates. Ask:

- Budget / funding envelope and any spent-to-date figure.
- Baseline start and end dates.
- Any assumptions the plan currently rests on (e.g. "vendor delivers by August", "funding
  approved for phase 2").
- Any dependencies on other teams, projects, or third parties.
- Any known risks (uncertain future events), and any current, already-happening problems (issues).

Write budget and baseline dates into `PROJECT.md` under **Hard facts**. Then seed the RAIDC items the
PM names. An interview yields one-liners, not fully-substantiated items — so seed everything the PM
gives you using the **proposed/provisional convention** (`registers/_schemas/risk.md` §2a): the agent
never invents an owner or a rating, it files a well-formed placeholder for the PM to confirm.

- For each stated **assumption**, seed `registers/assumptions/ASM-### Title.md` with
  `title, statement, owner, made(today), validate_by, validation_approach, status: unvalidated,
  impact_if_wrong`. If no owner or `validate_by` is given, file it with `owner: TBC`,
  `provisional: true`, an agent-suggested provisional `validate_by`, and note the gap in Open particulars.
- For each **dependency**, seed `registers/dependencies/DEP-### Title.md` with
  `title, description, direction(inbound|outbound), counterpart, owner, needed_by, criticality(1–3),
  status, linked_risk`. Use `owner: TBC` + `provisional: true` where the owner is not given.
- For each **risk** named, seed `registers/risks/RSK-### Title.md` with `status: proposed`,
  `provisional: true`, `owner: TBC`, a provisional (agent-suggested) `probability`/`impact` and
  `review` date, and a cause → risk → effect statement drafted from what the PM said. Confirm the
  ratings and owner are the PM's to set later.
- If the PM names a **current, already-happening problem**, seed an **issue**
  `registers/issues/ISS-### Title.md` with `status: proposed`, `provisional: true`, `owner: TBC` and a
  provisional `priority`/`target_date` — not a risk (it has already happened).

Everything seeded here is `proposed`/`provisional` until the PM confirms owners and ratings; list the
confirmations still needed in Open particulars.

## Handling unanswered questions

- Anything the human skips, defers, or cannot answer goes into a **`## Open particulars`** section
  at the bottom of `PROJECT.md` as a dated bullet (e.g. `- [ ] Delivery tolerances not yet set —
  asked 2026-07-22`). Never block, never guess, never fill a field to look complete.
- If a required register field is missing (an action with no owner, an assumption with no
  validate_by), file the item but flag the gap in Open particulars so the weekly review can chase it.

## Finish

1. Assign the next free ID in each register sequence (check existing files first; IDs are
   monotonic per prefix — RSK, ISS, ASM, DEP, CON, DEC, ACT, STK, REQ, DEL).
2. Set `updated: <today>` on every file you touched.
3. Regenerate `STATE.md` and any affected `views/` (stakeholder-map, raid) if register items were
   created.
4. Append a `log.md` entry: `## [YYYY-MM-DD] interview | Project particulars established` with the
   blocks covered, items seeded (with IDs), and the count of Open particulars.
5. Give the human a one-screen recap: what PROJECT.md now holds, which register items you seeded
   (by ID), and the Open particulars still to close. Do not present this as final — invite
   corrections; nothing here is baselined until they say so.
