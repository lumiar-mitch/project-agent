---
name: weekly-review
description: Use this for a weekly review, a Monday cadence check, or "what changed this week / this fortnight". Runs a stale sweep, a watermelon hunt, a register-quality sample, a movement summary with a top-3 worry list, and a governance-readiness check — then files a dated review and refreshes STATE.md.
---

# Weekly review

The recurring assurance pass. It surfaces what has gone stale, what looks greener than the evidence
supports, and what the next forum needs to decide. You produce a filed review and a refreshed
STATE.md; you do not change ratings, close items, or make decisions — those stay with the PM.

## Before you start

1. Read `STATE.md`, the latest review in `wiki/answers/` (for "since last review" comparison), and
   the `views/` tables.
2. Fix the window: since the last filed weekly review, or the last 7 days if none.
3. Today's date anchors every "past its date" test below.

## 1. Stale sweep

Scan the registers and list every item past its own date-driven trigger:

- **Risks** — `review` date in the past (review date is mandatory; a missing one is itself a finding).
- **Actions** — `due` in the past and `status` not done/cancelled (these are overdue by definition).
- **Assumptions** — `validate_by` in the past and still `unvalidated`.
- **Decisions** — `status: proposed` for more than 14 days with no forum date.
- **Stakeholders** — `sentiment_assessed` more than 45 days ago.

For each, give the ID, what's overdue, and by how long. This is a chase list for the human, not a
set of changes you make.

## 2. Watermelon hunt

Invoke the **status-drift** logic (`skills/status-drift`) across current status claims: any
green/amber with no observable evidence, any schedule slip sitting behind a green, any open severe
risk under an "on track", any estimate that has not moved across periods. Report each colour with
its supporting or contradicting evidence, per `standards/rag-evidence.md`. Frame red as a request
for support, not a failing.

## 3. Register-quality sample

Take a small sample (say 3–5 of the newest or most-changed items) and score them against the
relevant standard — `standards/risk-quality.md`, `standards/action-quality.md`,
`standards/decision-hygiene.md`, `standards/stakeholder-coverage.md`. Note quality gaps. Apply fixes
per the coaching posture (improve the register item, leave ratings to the human); the *pattern* goes
into the coaching digest at step 6, not instance-by-instance chatter here.

## 4. Movement + top-3 worries

- **Movement since last review:** what changed — items opened/closed, ratings proposed, decisions
  taken, dates moved. Draw it from register History and the views diff.
- **Top 3 things to worry about:** the three most material threats to the project right now. Each
  one must carry its **evidence** (register IDs, source citations with absolute dates) — no worry
  without a reason. Rank by materiality, not recency.

## 5. Governance readiness

Look ahead to the next governance forum (from PROJECT.md / governance-model). List the decisions
that will be pending for it: `status: proposed` decisions, tolerance breaches, risks needing
acceptance, and overdue actions the board should see. This previews what **governance-prep** will
build into the pack — flag if the pack should be started.

## Output

1. **File a dated review** in `wiki/answers/YYYY-MM-DD Weekly Review.md` with the five sections
   above. Cite everything.
2. **Refresh `STATE.md`** so it reflects the current picture (regenerate from registers/views; do
   not hand-edit generated blocks).
3. **Append a coaching digest to `wiki/coaching-log.md`** — *patterns, not instances*
   ("4 of 6 new risks this week arrived without owners — worth fixing the intake template?"). This
   is the graduation mechanism: recurring accepted lessons stop being explained per-item.
4. Append `wiki/log.md`: `## [YYYY-MM-DD] review | Weekly review` with the window, key findings, and
   the top-3 worries.
5. In chat, give the PM the headline: movement, the top-3 worries with evidence, the stale chase
   list, and what the next forum needs. The decisions and closures are theirs to make.
