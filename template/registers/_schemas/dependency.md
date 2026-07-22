# Dependency register — schema

## 1. Purpose

A **dependency** is a hand-off between this project and something outside its direct control — an input the project *needs* (inbound) or an output the project *owes* (outbound). The register tracks each hand-off, its counterpart, the date it is needed, and how critical it is. One file per dependency under `registers/dependencies/DEP-### Short title.md`. A slipping dependency typically spawns a linked [[risk]].

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `DEP-###` | yes | Immutable identifier. |
| `title` | string | yes | Short label naming the dependency — drives the `DEP-### <title>.md` filename. The fuller `description` is the secondary/body field. |
| `description` | string | yes | What is being handed over, in one line. |
| `direction` | `inbound` \| `outbound` | yes | Inbound = we need it from someone; outbound = someone needs it from us. |
| `counterpart` | string | yes | The external party/project/team on the other side of the hand-off. |
| `owner` | string — **a named person, never a team** (or `TBC` while unconfirmed) | yes | Named person on *our* side accountable for managing this dependency. May be `TBC` with `provisional: true` when created from a one-liner (see `risk.md` §2a); the agent never invents a name. |
| `needed_by` | date `YYYY-MM-DD` | yes | Date the hand-off must complete. Drives the stale/at-risk sweep. |
| `criticality` | integer 1–3 | yes | 1 = critical (blocks the critical path), 2 = major, 3 = minor. |
| `status` | `pending` \| `on-track` \| `at-risk` \| `met` \| `missed` | yes | Lifecycle of the hand-off. |
| `linked_risk` | string `RSK-###` | when at-risk | The risk raised for a slipping/threatened dependency; blank otherwise. |
| `provisional` | boolean `true` \| `false` (default `false`) | no | When `true`, `owner`/`needed_by`/`criticality` are agent-suggested, awaiting PM confirmation — see the canonical convention in `risk.md` §2a. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Related `ASM`/`CON`, `STK` counterpart, source. |

## 3. Body structure

- **The hand-off** — what exactly is exchanged, in which direction, and why the project depends on it.
- **Counterpart & interface** — who owns it on the other side, and how it is governed (contract, SLA, inter-project agreement).
- **Timing** — when it is needed and the lead time; note any float.
- **History** — dated log of status changes and date movements.

## 4. Worked example

```markdown
---
id: DEP-003
title: Vendor delivers signed-off integration API spec
description: Payroll vendor provides the finalised, signed-off integration API specification.
direction: inbound
counterpart: Northwind payroll vendor (via James Whitfield, account manager)
owner: Anita Kumar
needed_by: 2026-05-15
criticality: 1
status: at-risk
linked_risk: RSK-014
links: [ASM-005, CON-002, STK-009]
---

## The hand-off

We depend on the payroll vendor delivering the final integration API specification before we
can complete integration design. This is inbound and on the critical path for the Integration
workstream.

## Counterpart & interface

Owned by the vendor and managed through James Whitfield under the master services agreement.
Our contact for escalation is the sponsor, David Osei (STK-004).

## Timing

Needed by 2026-05-15 to protect design sign-off. As of 2026-04-22 the spec is two weeks late
and the real-time capability is now in doubt (see ASM-005) — status set to at-risk and RSK-014
raised.

## History

- 2026-01-30 Logged as pending, criticality 1.
- 2026-04-22 Slipped; status → at-risk; linked to RSK-014.
```

## 5. Processing rule

When a dependency arrives — from an uploaded register, a meeting, or chat:

1. **Validate against `standards/risk-quality.md`.** Require `direction`, a named `owner` on *our* side, a `counterpart`, a `needed_by` date, and `criticality`.
2. **Coach (FULL coaching).** If a "dependency" is really an internal task, reframe it as an `ACT`. If direction or counterpart is missing, ask. Leave a coach's note.
3. **Dedupe** against open dependencies.
4. **Auto-spawn / link.** On `status: at-risk` or `missed`, raise or link a `RSK` (set `linked_risk`) and tell the PM. Cross-link the counterpart to an `STK` where one exists.
5. Flag dependencies past `needed_by` and still un-`met` in the weekly stale sweep.
6. File as received in `raw/`, write the improved version to the register, regenerate `views/raid.md`, and report before/after.
