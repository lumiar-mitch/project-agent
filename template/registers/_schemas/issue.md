# Issue register — schema

## 1. Purpose

An **issue** is a problem that *has already happened* (or is happening now) and is affecting the project — no uncertainty, it is real. One file per issue under `registers/issues/ISS-### Short title.md`. Issues often arrive as a realised [[risk]] (`RSK`) or as a fresh problem raised in a meeting.

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `ISS-###` | yes | Immutable identifier. |
| `title` | string | yes | Short noun phrase naming the problem. |
| `status` | `proposed` \| `open` \| `investigating` \| `resolving` \| `resolved` \| `closed` | yes | Lifecycle. `proposed` = created from a one-liner, not yet PM-confirmed (see the proposed/provisional convention in `risk.md` §2a). `resolved` = fix applied; `closed` = confirmed and verified. |
| `owner` | string — **a named person, never a team** (or `TBC` while `proposed`) | yes | Single accountable individual driving resolution. May be `TBC` while `status: proposed`; must be named before it moves to `open`. |
| `raised` | date `YYYY-MM-DD` | yes | When the issue was logged. |
| `target_date` | date `YYYY-MM-DD` | yes | Committed resolution date. Drives the stale/overdue sweep. |
| `resolved` | date `YYYY-MM-DD` | when resolved | Actual resolution date; blank while open. |
| `priority` | integer 1–4 | yes | 1 = critical/urgent, 4 = low. Drives triage order. |
| `impact` | string | yes | Concrete effect on scope, schedule, cost, or quality (what is actually happening). |
| `workstream` | string | yes | Which workstream/area it sits in. |
| `from_risk` | string `RSK-###` | when spawned | The risk that realised into this issue; blank if raised directly. |
| `provisional` | boolean `true` \| `false` (default `false`) | no | When `true`, `owner` and/or `priority`/`target_date` are agent-suggested, awaiting PM confirmation — see the canonical convention in `risk.md` §2a. Pairs with `status: proposed`. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Resolving `ACT`s, related `DEC`, source meeting. |

## 3. Body structure

- **What happened** — a factual statement of the problem in the present/past tense (no "might"): what occurred, when, and how it was detected.
- **Impact** — the concrete consequence on objectives right now, and who/what is affected.
- **Resolution** — bulleted list of linked `ACT-###` items driving the fix, plus any `DEC-###` taken. Preferred over prose.
- **History** — dated log of status transitions and priority changes.

## 4. Worked example

```markdown
---
id: ISS-007
title: Interface batch to General Ledger failing nightly
status: resolving
owner: Anita Kumar
raised: 2026-07-08
target_date: 2026-07-24
resolved:
priority: 1
impact: Finance cannot post daily labour cost to the GL; month-end close at risk.
workstream: Integration
from_risk: RSK-021
links: [ACT-041, DEC-012, "[[meetings/2026-07-08 Incident review]]"]
---

## What happened

Since the 2026-07-06 release, the nightly Meridian → GL batch has failed with a schema
mismatch on the cost-centre field. Detected 2026-07-08 when Finance reported two missing
daily postings.

## Impact

Daily labour-cost postings to the General Ledger have stopped. If unresolved by 2026-07-24,
the July month-end close cannot be reconciled on time and manual journals will be required.

## Resolution

- [[ACT-041]] Patch the cost-centre field mapping and re-run failed batches (owner: Anita Kumar, due 2026-07-22).
- [[DEC-012]] Agreed to hold GL cutover until three clean nightly runs are evidenced.

## History

- 2026-07-08 Raised P1 from realised risk RSK-021.
- 2026-07-12 Root cause confirmed (unmapped cost-centre); status → resolving.
```

## 5. Processing rule

When an issue arrives — from an uploaded register, a meeting, chat, or a realised risk:

1. **Validate against `standards/risk-quality.md`** (the RAIDC quality standard). Confirm required fields, a *named* `owner`, and a `target_date`. When the issue can only be created from a one-liner (e.g. an interview mention of a current, already-happening problem), file it as `status: proposed` + `provisional: true` with `owner: TBC` and a provisional `priority`/`target_date` per the convention in `risk.md` §2a — never invent the owner or the ratings.
2. **Distinguish issue from risk (FULL coaching).** If the item is actually *uncertain* (hasn't happened), reframe it as a `RSK` and tell the PM why. If it is a realised risk, ensure `from_risk` points at the originating `RSK` and that the risk is marked `realised`/`closed`.
3. **Dedupe** against open issues before creating a new file.
4. **Auto-link.** Each resolution step should be a real `ACT` with owner + due date; create/link them. Link any `DEC` taken.
5. On `status: resolved`, set `resolved` date; on `closed`, confirm verification. Regenerate `views/raid.md`.
6. File as received in `raw/`, write the improved version to the register, and report before/after with a pointer to the standard.
