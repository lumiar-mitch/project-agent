# Action register — schema

## 1. Purpose

An **action** is a discrete piece of work assigned to *one person* with *one due date*. The register is the project's to-do source of truth, feeding `views/actions.md`. One file per action under `registers/actions/ACT-### Short title.md`. **No owner or no due date → it is not yet an action; the agent asks for both before filing.**

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `ACT-###` | yes | Immutable identifier. |
| `description` | string | yes | The work to do, as an imperative starting with a verb ("Cleanse allowance codes…"). |
| `owner` | string — **a named person, never a team** | **yes** | Single accountable person. Missing → not an action; the agent asks who. |
| `due` | date `YYYY-MM-DD` | **yes** | Committed completion date. Missing → not an action; the agent asks by when. |
| `status` | `open` \| `done` \| `overdue` \| `cancelled` | yes | Lifecycle. `overdue` is agent-derived when `due` passes while `open`. |
| `raised` | date `YYYY-MM-DD` | yes | When the action was created. |
| `origin` | string / ID | yes | Where it came from: a meeting, `chat`, an ingest, or a parent item (`RSK-###`, `ISS-###`, `DEC-###`). |
| `workstream` | string | yes | Which workstream/area it sits in. |
| `closed` | date `YYYY-MM-DD` | when done/cancelled | Actual completion or cancellation date. |
| `closure_note` | string | when done/cancelled | One line on what was delivered or why cancelled. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Parent `RSK`/`ISS`/`DEC`, related items, evidence. |

## 3. Body structure

Actions are usually short and can live in frontmatter alone. Use the body when there is more to say:

- **Detail** — any elaboration on the work, acceptance/"done" criteria.
- **Progress** — dated updates while open.
- **Closure** — what was delivered (evidence link) on completion.

## 4. Worked example

```markdown
---
id: ACT-032
description: Profile and cleanse legacy allowance codes against the current award before extract
owner: Tom Fitzgerald
due: 2026-06-30
status: open
raised: 2026-05-12
origin: RSK-014
workstream: Data Migration
closed:
closure_note:
links: [RSK-014, ASM-005]
---

## Detail

Run data profiling across all 240 legacy allowance codes, map each to a current award code,
and flag orphans for SME review. **Done when** every active code is mapped or retired and the
exception list is signed off by Michael Brennan.

## Progress

- 2026-05-28 Profiling complete; 31 orphan codes found.
- 2026-06-18 22 of 31 resolved with payroll SME; 9 pending award interpretation.
```

## 5. Processing rule

When an action arrives — from a meeting, an uploaded register, chat, or as a mitigation on another item:

1. **Validate against `standards/action-quality.md`.** The two hard gates: a **named `owner`** and a **`due` date**. If either is missing, the item is *not an action yet* — the agent batch-asks "who owns this?" and "by when?" and does not file a headless/undated action.
2. **Coach (FULL coaching).** Rewrite vague descriptions ("look into migration") into a verb-led, outcome-clear imperative with a "done" criterion, and leave a coach's note pointing to `action-quality`. Reject a team as owner — ask for the individual.
3. **Set `origin`.** Tag `chat` for captured-from-chat actions; link the parent `RSK`/`ISS`/`DEC` where the action is a mitigation/resolution step.
4. **Dedupe** against open actions.
5. **Derive `overdue`.** When `due` passes and status is still `open`, the agent flips it to `overdue` and surfaces it in the weekly stale sweep. (The human owns closing/accepting an action; the agent tracks and nudges.)
6. On `done`/`cancelled`, set `closed` and `closure_note`. File as received in `raw/` where applicable, write to the register, regenerate `views/actions.md`, and report.
