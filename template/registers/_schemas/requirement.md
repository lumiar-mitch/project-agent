# Requirement register — schema

## 1. Purpose

A **requirement** is a stated need the solution must meet, traceable from its source to the deliverable that satisfies it. The register makes scope explicit, prioritised, and owned. One file per requirement under `registers/requirements/REQ-### Short title.md`. Requirements link to the deliverable (`DEL-###`) that fulfils them and to the `DEC`s that shape scope.

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `REQ-###` | yes | Immutable identifier. |
| `title` | string | yes | Short name for the requirement. |
| `type` | `functional` \| `non-functional` \| `acceptance` | yes | What kind of requirement it is. |
| `deliverable` | string `DEL-###` | yes | The deliverable that satisfies this requirement (traceability link). |
| `priority` | `must` \| `should` \| `could` \| `wont` (MoSCoW) | yes | Prioritisation. `wont` = explicitly out of scope this release. |
| `status` | `proposed` \| `accepted` \| `in-progress` \| `delivered` \| `verified` \| `dropped` | yes | Lifecycle from raised to verified against acceptance. |
| `source` | string / citation | yes | Where the requirement came from (person, document, `DEC`, workshop) — with a date. |
| `owner` | string — **a named person, never a team** | yes | Named person accountable for the requirement (typically a business owner / product owner). |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Related `ASM`/`CON`/`RSK`/`DEC`, acceptance criteria, source. |

## 3. Body structure

- **Requirement** — a clear, testable statement in the form "The solution must/should …". Avoid solutioning; state the need.
- **Acceptance criteria** — how "met" is proven (for `type: acceptance`, this is the core). Testable and unambiguous.
- **Traceability** — source → requirement → `DEL-###` deliverable; note any `DEC` that scoped it in or out.
- **History** — dated status changes.

## 4. Worked example

```markdown
---
id: REQ-021
title: Approved rosters visible to payroll within 15 minutes
type: non-functional
deliverable: DEL-007
priority: should
status: in-progress
source: Workshop with rostering managers, 2026-02-15
owner: Rebecca Lawson
links: [ASM-005, DEP-003, ISS-018, "[[foundation/scope]]"]
---

## Requirement

The solution should make an approved roster available to the payroll engine within 15 minutes
of approval, so late shift changes are paid correctly in the same cycle.

## Acceptance criteria

- A roster approved at any time is queryable in payroll within 15 minutes, measured across a
  one-week soak test.
- Failed transfers raise an alert to the integration owner.

## Traceability

Source: rostering-managers workshop (2026-02-15) → REQ-021 → DEL-007 (Integration build).
Threatened by the invalidated real-time-API assumption (ASM-005); scope decision pending (ISS-018).

## History

- 2026-02-15 Raised (should).
- 2026-04-22 At risk after ASM-005 invalidated; batch-only fallback under review.
```

## 5. Processing rule

When a requirement arrives — from an uploaded backlog/register, a workshop, a charter, or chat:

1. **Validate against `standards/risk-quality.md`** (the general register-quality standard for non-RAID items). Require `type`, `priority` (MoSCoW), a `source` with a date, a named `owner`, and a `deliverable` traceability link (create a `DEL` stub if none exists).
2. **Coach (FULL coaching).** Rewrite solutioned or untestable requirements ("use a fast database") into a need with acceptance criteria, and leave a coach's note. For `acceptance` requirements, insist on testable criteria.
3. **Dedupe** against existing requirements; merge near-duplicates.
4. **Traceability check.** Every requirement must trace to a `DEL`; flag orphan requirements (no deliverable) and orphan deliverables (no requirement) in the review. Link `ASM`/`CON`/`RSK` that affect feasibility.
5. **Human owns acceptance.** The agent records status and improves the write-up; sign-off to `verified` and any scope change (`dropped`, MoSCoW re-prioritisation) is a human decision, ideally recorded as a `DEC`.
6. File as received in `raw/`, write the improved version to the register, update `wiki/foundation/scope.md`, regenerate any requirements view, and report before/after.
