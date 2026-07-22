# Risk register — schema

## 1. Purpose

A **risk** is an *uncertain* future event that, if it occurs, would affect the project's objectives. The risk register is the source of truth for every open threat and opportunity: one file per risk under `registers/risks/RSK-### Short title.md`. Something that has *already happened* is not a risk — it is an [[issue]] (`ISS`), and the agent reframes it.

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `RSK-###` (zero-padded 3 digits) | yes | Immutable identifier. Never reused. |
| `title` | string | yes | Short noun phrase naming the risk (not the cause, not the effect). |
| `type` | `threat` \| `opportunity` | yes | Downside risk or upside risk. Defaults to `threat`. |
| `status` | `proposed` \| `open` \| `mitigating` \| `closed` \| `realised` | yes | Lifecycle. `realised` = it occurred → auto-spawns a linked `ISS`. |
| `owner` | string — **a named person, never a team** | yes | Single accountable individual who manages the response. A team/role is rejected and the agent asks who. |
| `raised_by` | string (person) | yes | Who first surfaced the risk. |
| `raised` | date `YYYY-MM-DD` | yes | When it was logged. |
| `review` | date `YYYY-MM-DD` | **yes (mandatory)** | Next review date. Drives the stale sweep — a risk past its review date is flagged in the weekly review. |
| `probability` | integer 1–5 | yes | Likelihood. 1 = rare, 5 = almost certain. Owner/PM owns this rating; agent may advise. |
| `impact` | integer 1–5 | yes | Severity of effect on objectives if it occurs. 1 = negligible, 5 = severe. |
| `severity` | integer 1–25 + band, **agent-maintained** | derived | `probability × impact`. Agent recomputes on every edit; PM does not hand-set it. Bands: 1–4 low, 5–9 medium, 10–14 high, 15–25 critical. |
| `proximity` | `imminent` \| `near` \| `medium` \| `distant` (or a date) | yes | How soon the risk could materialise. A date is preferred when known. |
| `response` | `avoid` \| `reduce` \| `transfer` \| `accept` | yes | Chosen response strategy (for opportunities read as exploit/enhance/share/accept). |
| `workstream` | string | yes | Which workstream/area it sits in. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Related items: mitigating `ACT`s, source meetings, spawned `ISS`, related `ASM`/`DEP`. |

## 3. Body structure

- **Risk statement** — a single structured **cause → risk → effect** sentence:
  *"Because &lt;fact/cause that is true today&gt;, &lt;uncertain event&gt; may occur, leading to &lt;effect on objectives&gt;."*
  The cause is a certainty, the risk is the uncertainty, the effect is the consequence. Fused "the project might be late" statements get reframed.
- **Mitigations** — bulleted list of linked `ACT-###` items (each a real action with an owner and due date). Distinguish *preventive* (reduce probability) from *contingent* (reduce impact) where useful.
- **History** — dated log of score changes, response changes, and status transitions, so the git diff is legible in prose too.

## 4. Worked example

```markdown
---
id: RSK-014
title: Payroll data migration data-quality shortfall
type: threat
status: mitigating
owner: Tom Fitzgerald
raised_by: Priya Nair
raised: 2026-03-04
review: 2026-08-01
probability: 4
impact: 5
severity: 20 (critical)
proximity: near
response: reduce
workstream: Data Migration
links: [ACT-032, ACT-037, ASM-005, "[[meetings/2026-03-04 Migration workshop]]"]
---

## Risk statement

Because the legacy rostering system has 11 years of un-validated allowance codes and no
enforced referential integrity, incorrect or incomplete pay data may be migrated into
Meridian, leading to underpayment or overpayment of staff at first go-live pay run and a
reportable payroll compliance breach.

## Mitigations

- **Preventive** — [[ACT-032]] Profile and cleanse allowance codes against the award before
  extract (owner: Tom Fitzgerald, due 2026-06-30).
- **Preventive** — [[ACT-037]] Build automated reconciliation of gross-to-net for a 3-pay
  parallel run (owner: Michael Brennan, due 2026-07-15).
- **Contingent** — manual pay-correction runbook and a funded contingency pay run held for
  the first two cycles.

## History

- 2026-03-04 Raised at migration workshop; P4×I5 = 20 (critical).
- 2026-05-12 Response set to *reduce*; ACT-032 and ACT-037 opened.
- 2026-07-10 Status → mitigating after cleanse pass 1; probability held at 4 pending parallel-run evidence.
```

## 5. Processing rule

When a risk arrives — from an uploaded register, a meeting, or chat:

1. **Validate against `standards/risk-quality.md`.** Check required fields are present, that `owner` is a *named person* (reject a team — ask who), and that a `review` date exists (mandatory).
2. **Reframe weak forms (FULL coaching).** If the statement is a fused one-liner, rewrite it into cause → risk → effect and leave a coach's note showing before/after and the "why" (pointing to `risk-quality`). If the item describes something that has *already happened*, reframe it as an issue, tell the PM why, and file it as an `ISS` instead.
3. **Recompute `severity`** = probability × impact and set the band. The agent maintains this field; the PM/owner own the probability and impact *ratings* (accountability line: the agent advises and improves the write-up, the human owns the numbers and the decision).
4. **Dedupe** against open risks before creating a new file; if it matches an existing risk, update that item's History rather than duplicating.
5. **Auto-spawn / link.** On `status: realised`, auto-create a linked issue (`from_risk: RSK-###`) and set the risk `closed`. Ensure each mitigation is a real `ACT` with owner + due date; create the `ACT` stubs and link them.
6. File the artefact as received in `raw/` (immutable), write the improved version to the register, regenerate `views/raid.md`, and report the before/after to the PM.
