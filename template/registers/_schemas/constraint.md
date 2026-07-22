# Constraint register — schema

## 1. Purpose

A **constraint** is a fixed boundary the project must work within — a limit on time, cost, scope, resource, or a regulatory/technical rule — that is *not* the project's to change. The register records each boundary, who set it, whether it can be negotiated, and what it forces. One file per constraint under `registers/constraints/CON-### Short title.md`. Constraints shape plans and frequently sit behind [[risk]]s and [[assumption]]s.

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `CON-###` | yes | Immutable identifier. |
| `statement` | string | yes | The boundary, stated as a hard limit ("Go-live must be on or before…"). |
| `category` | `time` \| `cost` \| `scope` \| `resource` \| `regulatory` \| `technical` | yes | Type of boundary. |
| `authority` | string | yes | Who imposed it (the source of the constraint — a person, body, contract, or law). |
| `negotiable` | boolean `true` \| `false` | yes | Whether it can be challenged/changed, and by whom if so (note in body). |
| `implications` | string | yes | What the constraint forces the project to do or forgo. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Related `RSK`/`ASM`/`DEP`/`DEC`, source. |

## 3. Body structure

- **Constraint** — the boundary as a hard statement, with the value/limit made explicit.
- **Authority & basis** — who set it and on what basis (contract clause, regulation, board mandate, budget envelope).
- **Implications** — how it shapes the plan: what it rules out, what it forces, and any `RSK`/`ASM` it drives.
- **Negotiability** — if negotiable, who can change it and through what forum; if not, say so plainly.

## 4. Worked example

```markdown
---
id: CON-002
title: Go-live must precede the new financial year
statement: Meridian must be live in production on or before 2026-09-30, ahead of the FY2027 pay cycle.
category: time
authority: David Osei (Executive Sponsor), endorsed by the Board 2026-01-20
negotiable: false
implications: No schedule float beyond September; parallel-run window is compressed to three pay cycles; scope must flex, not the date.
links: [RSK-014, DEP-003, DEC-009]
---

## Constraint

Meridian must be in production **on or before 30 September 2026**, so the first FY2027 pay run
executes on the new platform.

## Authority & basis

Set by the Executive Sponsor (David Osei) and endorsed by the Board on 2026-01-20. It is tied
to the financial-year boundary and payroll compliance reporting.

## Implications

The date is fixed, so scope is the flex variable. It compresses the parallel-run window to three
pay cycles and directly raises the migration data-quality risk (RSK-014). Any slip in the vendor
API dependency (DEP-003) threatens this date.

## Negotiability

Not negotiable at project level. A change would require Board approval via the sponsor.
```

## 5. Processing rule

When a constraint arrives — from an uploaded register, a meeting, a charter, or chat:

1. **Validate against `standards/risk-quality.md`** (the RAIDC quality standard). Require a `category`, an `authority` (a constraint with no source is suspect — the agent asks who set it), and `negotiable` set explicitly.
2. **Coach (FULL coaching).** If a "constraint" is really a *choice* the project could change, reframe it (often as a `DEC` or an `ASM`) and tell the PM. Ensure the statement carries the actual limit/value, not a vague "budget is tight".
3. **Dedupe** against open constraints.
4. **Link, don't spawn.** Constraints rarely auto-spawn, but the agent links the `RSK`s and `ASM`s a constraint drives, and any `DEC` that would be needed to change a `negotiable: true` constraint.
5. **No mandatory review date**, but constraints are re-checked at each stage gate for continued validity.
6. File as received in `raw/`, write the improved version to the register, regenerate `views/raid.md`, and report before/after.
