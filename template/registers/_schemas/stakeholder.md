# Stakeholder register — schema

## 1. Purpose

A **stakeholder** is any person (or clearly-bounded body) with influence over, or interest in, the project. The register holds each stakeholder's power/interest position, current sentiment, and engagement approach — feeding `views/stakeholder-map.md`. One file per stakeholder under `registers/stakeholders/STK-### Name.md`. Sentiment older than ~45 days shows as stale and prompts a re-read.

## 2. Frontmatter schema

| field | type / enum | required? | description |
|---|---|---|---|
| `id` | string `STK-###` | yes | Immutable identifier. |
| `name` | string | yes | The stakeholder's name. This is the label that drives the `STK-### <name>.md` filename — the title-equivalent for a person (a stakeholder has a name, not a `title`). |
| `role` | string | yes | Their role/title relevant to the project. |
| `org` | string | yes | Their organisation or business unit. |
| `category` | `sponsor` \| `governance` \| `user` \| `supplier` \| `regulator` \| `delivery` \| `impacted` | yes | Type of stakeholder relationship. |
| `influence` | integer 1–5 | yes | Power over project outcomes. 1 = low, 5 = high. |
| `interest` | integer 1–5 | yes | How much the outcome matters to them. 1 = low, 5 = high. |
| `sentiment` | `champion` \| `supportive` \| `neutral` \| `resistant` \| `hostile` | yes | Current stance toward the project. |
| `sentiment_assessed` | date `YYYY-MM-DD` | yes | When sentiment was last judged. >~45 days old shows as stale. |
| `engagement` | `manage-closely` \| `keep-satisfied` \| `keep-informed` \| `monitor` | derived | Agent-derived from the influence×interest grid. |
| `comms_cadence` | string | yes | How often and how they are engaged (e.g. "weekly 1:1", "monthly SteerCo pack"). |
| `key_concerns` | string / list | yes | What they most care about or worry about — drives messaging. |
| `links[]` | list of IDs / `[[wikilinks]]` / raw citations | no | Related `DEC`/`DEP`/`RSK`, `wiki/people/` page, source. |

## 3. Body structure

- **Position** — a short read of where they sit: influence/interest and why, mapped to the engagement quadrant.
- **Sentiment & drivers** — current stance and *why*, with evidence and date; what would move them.
- **Engagement plan** — how they are kept engaged (cadence, channel, messenger), and any asks of them.
- **History** — dated log of sentiment/position changes.

## 4. Worked example

```markdown
---
id: STK-004
name: David Osei
role: Executive Sponsor (CFO)
org: Northwind Health
category: sponsor
influence: 5
interest: 4
sentiment: supportive
sentiment_assessed: 2026-07-15
engagement: manage-closely
comms_cadence: Fortnightly 1:1 + monthly SteerCo
key_concerns: Fixed FY go-live (CON-002); no payroll compliance breach; cost held to budget.
links: [DEC-009, CON-002, RSK-014, "[[people/David Osei]]"]
---

## Position

High influence (holds budget and the go-live mandate) and high interest (payroll accuracy is a
CFO reputational item). Firmly in **manage-closely**.

## Sentiment & drivers

Supportive as of 2026-07-15 — endorsed the big-bang decision (DEC-009) and defends the FY date.
Would turn resistant if the migration data-quality risk (RSK-014) is seen to threaten a
compliant first pay run. Moved by clear evidence of parallel-run reconciliation.

## Engagement plan

Fortnightly 1:1 with the PM plus the monthly SteerCo pack. Ask of him: hold the Board line on
scope-flex-not-date. Messenger for vendor escalation on DEP-003.

## History

- 2026-01-20 Secured Board endorsement of the date.
- 2026-05-20 Chaired the go-live approach decision (DEC-009).
- 2026-07-15 Sentiment reaffirmed supportive.
```

## 5. Processing rule

When a stakeholder arrives — from an uploaded register, a meeting, an org chart, or chat:

1. **Validate against `standards/stakeholder-coverage.md`.** Require `role`, `org`, `category`, `influence`, `interest`, `sentiment`, and `sentiment_assessed`. Flag coverage gaps (e.g. a named sponsor with no register entry, or a category with no stakeholders).
2. **Derive `engagement`** from the influence×interest grid: high/high → manage-closely, high/low → keep-satisfied, low/high → keep-informed, low/low → monitor. Agent maintains this field; the *sentiment* rating is a human judgement the agent records and prompts on, not one it invents.
3. **Coach (FULL coaching).** If sentiment is asserted without a basis, ask for the evidence and date; leave a coach's note. Reframe a team ("Finance") into the actual named influencers where possible.
4. **Dedupe** against existing stakeholders (match on name + org).
5. **Stale sweep.** Sentiment older than ~45 days is flagged for re-assessment in the weekly review.
6. File as received in `raw/`, write the improved version to the register, regenerate `views/stakeholder-map.md`, optionally cross-link a `wiki/people/` page, and report.
