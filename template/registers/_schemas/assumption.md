# Assumption register — schema

## 1. Purpose

An **assumption** is something taken to be true, for planning purposes, that has *not yet been validated*. The register makes each assumption explicit, owned, and time-boxed to a validation date — so an unexamined belief cannot quietly become a project failure. One file per assumption under `registers/assumptions/ASM-### Short title.md`. An `invalidated` assumption **must** spawn a downstream item: an [[issue]] for any impact already realised, and/or a [[risk]] for any residual forward exposure — both when both apply (see the processing rule).

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `ASM-###` | yes | Immutable identifier. |
| `title` | string | yes | Short label naming the assumption — drives the `ASM-### <title>.md` filename. The fuller `statement` is the secondary/body field. |
| `statement` | string | yes | The thing assumed true, stated plainly and testably. |
| `owner` | string — **a named person, never a team** (or `TBC` while unconfirmed) | yes | Who is accountable for validating it. May be `TBC` with `provisional: true` when created from a one-liner (see `risk.md` §2a); the agent never invents a name. |
| `made` | date `YYYY-MM-DD` | yes | When the assumption was recorded. |
| `validate_by` | date `YYYY-MM-DD` | yes | Deadline to confirm or disprove. Drives the stale sweep — past this date and still `unvalidated` is flagged. |
| `validation_approach` | string | yes | How it will be tested (who to ask, what evidence settles it). |
| `status` | `unvalidated` \| `validated` \| `invalidated` | yes | Lifecycle. `invalidated` must spawn a downstream `ISS` (realised impact) and/or `RSK` (residual exposure) — both when both apply. |
| `impact_if_wrong` | string | yes | What breaks if the assumption proves false — the reason it matters. |
| `provisional` | boolean `true` \| `false` (default `false`) | no | When `true`, `owner`/`validate_by` are agent-suggested, awaiting PM confirmation — see the canonical convention in `risk.md` §2a. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Spawned `RSK`/`ISS`, related `DEP`/`CON`, source. |

## 3. Body structure

- **Assumption** — the statement in full, framed so it can be proven true or false ("We assume X; if X is false, Y").
- **Why we're assuming it** — the basis (no evidence yet, awaiting confirmation, industry norm, prior project).
- **Validation** — the approach, who owns it, and the target date; updated with the evidence when tested.
- **History** — dated log of status changes and validation findings.

## 4. Worked example

```markdown
---
id: ASM-005
title: Payroll vendor exposes a real-time roster API
statement: The Meridian payroll vendor provides a documented real-time API to push approved rosters (not a nightly file only).
owner: Anita Kumar
made: 2026-02-18
validate_by: 2026-04-30
validation_approach: Obtain the vendor API spec and run a sandbox call in the integration environment before design sign-off.
status: invalidated
impact_if_wrong: The real-time rostering requirement (REQ-021) cannot be met; integration must fall back to batch, forcing a design change and schedule impact.
links: [RSK-014, ISS-018, REQ-021, DEP-003]
---

## Assumption

We assumed the payroll vendor offers a real-time roster API. If it only supports a nightly
batch file, the "rosters visible within 15 minutes" requirement is not achievable as designed.

## Why we're assuming it

Stated verbally by the vendor account manager during selection; never confirmed against the
API documentation.

## Validation

Anita Kumar to obtain the API spec and run a sandbox call before design sign-off (target
2026-04-30). **Finding 2026-04-22:** the vendor supports batch file only; no real-time API.
Assumption **invalidated** → raised ISS-018 (design change) and linked to RSK-014.

## History

- 2026-02-18 Recorded as unvalidated at design kickoff.
- 2026-04-22 Invalidated by vendor documentation; spawned ISS-018.
```

## 5. Processing rule

When an assumption arrives — from an uploaded register, a meeting, or chat:

1. **Validate against `standards/risk-quality.md`.** Require a *named* `owner`, a `validate_by` date, and a `validation_approach`. An assumption with no owner or no validation date is incomplete — the agent asks for both.
2. **Coach the framing (FULL coaching).** Rewrite vague assumptions ("resourcing will be fine") into a testable statement with an explicit `impact_if_wrong`, and leave a coach's note.
3. **Dedupe** against open assumptions.
4. **Auto-spawn (hard rule).** On `status: invalidated`, never leave the assumption without a downstream item. Decide by what the invalidation has actually done:
   - If it has **already caused a problem** → spawn an `ISS` for the realised impact.
   - If **forward uncertainty remains** → spawn an `RSK` for the residual exposure.
   - If **both apply** (a problem has landed *and* more could follow) → spawn **both**: an `ISS` for the realised impact and an `RSK` for the residual exposure. This both-apply case is the common one; do not force a single choice.
   Link every spawned item back to the assumption, and — when both are spawned — link the `ISS` and `RSK` to each other. Set `links`, and tell the PM.
5. Flag assumptions past `validate_by` in the weekly stale sweep.
6. File as received in `raw/`, write the improved version to the register, regenerate `views/raid.md`, and report before/after.
