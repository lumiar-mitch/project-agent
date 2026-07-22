# Decision register — schema

## 1. Purpose

A **decision** is a committed choice between options, made by a named authority in a named forum. The register is the project's decision log and audit trail: what was chosen, by whom, why, and what it resolves. One file per decision under `registers/decisions/DEC-### Short title.md`. A `decided` decision is **immutable** except by a later decision that supersedes it. A decision with only one option considered gets coached.

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `DEC-###` | yes | Immutable identifier. |
| `title` | string | yes | The question decided, as a short noun phrase. |
| `status` | `proposed` \| `pending` \| `decided` \| `superseded` | yes | Lifecycle. `decided` is immutable; only a superseding `DEC` changes it. |
| `decided_by` | string (named person/authority) | yes when decided | Who holds the decision — a named person or accountable role-holder. |
| `forum` | string | yes | Where it was taken (e.g. SteerCo, Sponsor, Design Authority, PM). |
| `date` | date `YYYY-MM-DD` | yes when decided | Date the decision was made. |
| `resolves[]` | list of IDs | no | The `RSK`/`ISS`/`ASM`/`DEP`/`REQ` items this decision closes out or answers. |
| `supersedes` | string `DEC-###` | when superseding | The prior decision this one replaces; sets that decision's status to `superseded`. |
| `review` | date `YYYY-MM-DD` | no | Optional date to revisit (e.g. for a provisional/time-bound decision). Drives the stale sweep for `proposed`/`pending` decisions. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Governance pack, meeting minutes, related items. |

## 3. Body structure

- **Decision** — the choice made, in one sentence.
- **Options considered** — **required.** A list of the genuine alternatives (minimum two), each with a one-line pro/con. A single-option "decision" is not a decision; the agent coaches for the discarded alternatives.
- **Rationale** — why the chosen option won, against the options above.
- **Source citation** — link to the forum/meeting where it was taken, with an absolute date (`[[governance/…]]` or a raw citation).
- **History** — status transitions (proposed → decided → superseded).

## 4. Worked example

```markdown
---
id: DEC-009
title: Migration approach — phased by pay group vs big-bang
status: decided
decided_by: David Osei (Executive Sponsor)
forum: Steering Committee
date: 2026-05-20
resolves: [RSK-014, ASM-005]
supersedes:
review:
links: ["[[governance/2026-05-20 SteerCo pack]]", CON-002]
---

## Decision

Migrate to Meridian **big-bang across all pay groups** at a single go-live, with a three-cycle
parallel run, rather than phasing by pay group.

## Options considered

- **Big-bang, all pay groups (chosen)** — pro: single reconciliation, meets the FY deadline
  (CON-002); con: higher first-run risk, no fallback between phases.
- **Phased by pay group** — pro: contains blast radius, learn-and-adjust; con: dual-run of two
  payroll systems for ~4 months, breaches the FY go-live constraint (CON-002).
- **Phased by site** — pro: geographic containment; con: allowances are award-based not
  site-based, so it does not reduce the core data-quality risk (RSK-014).

## Rationale

The fixed FY2027 go-live (CON-002) rules out a long phased dual-run. Big-bang is chosen because
the residual risk (RSK-014) is being reduced by the cleanse and parallel-run mitigations, and a
phased approach would breach the immovable date without materially lowering data-quality risk.

## Source citation

Steering Committee, 2026-05-20 ([[governance/2026-05-20 SteerCo pack]]).

## History

- 2026-05-06 Proposed to SteerCo.
- 2026-05-20 Decided (big-bang) by sponsor in SteerCo.
```

## 5. Processing rule

When a decision arrives — from an uploaded register, a governance pack, a meeting, or chat:

1. **Validate against `standards/decision-hygiene.md`.** Require `forum`, and (when `status: decided`) `decided_by` and `date`. Require an **options considered** section with at least two genuine alternatives.
2. **Coach (FULL coaching).** A single-option decision is reframed: the agent asks what alternatives were weighed and what was rejected, and leaves a coach's note pointing to `decision-hygiene`. If the record lacks rationale or a source, it prompts for them.
3. **Dedupe** against existing decisions.
4. **Immutability + supersede.** Never edit a `decided` decision's choice. A change is a *new* `DEC` with `supersedes: DEC-###`; the agent sets the old one to `superseded` and links them. (The human owns the decision itself — the agent records, cross-links, and improves the write-up, but never makes or alters the call.)
5. **Auto-link `resolves[]`.** Close or update any `RSK`/`ISS`/`ASM`/`DEP`/`REQ` the decision resolves, and note the `DEC` on those items.
6. File as received in `raw/`, write the improved version to the register, regenerate `views/decisions.md`, and report before/after.
