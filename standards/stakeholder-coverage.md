# Standard: Stakeholder coverage

*Applies to `registers/stakeholders/` (STK) and `wiki/people/`. Referenced by the weekly review,
`governance-prep`, and SOUL principles 4 and 9.*

## 1. The principle

Projects don't fail on delivery alone — they fail because a stakeholder who mattered was surprised at
the end. **Perception is reality**, and success is *stakeholder-conferred*: a project delivered on
time and budget is still a failure if the people who matter believe it failed. That means stakeholder
sentiment is not a start-up exercise you do once — it decays, and it must be **freshly assessed and
continuously realigned** so there are no end-of-project surprises. The agent's job is to keep the map
honest: every high-influence stakeholder has a current sentiment reading and a live engagement
strategy, and any high-influence stakeholder with no engagement plan is flagged as a gap, not left to
chance.

## 2. The checklist

For the stakeholder register (STK) as a whole and each entry:

- [ ] **Influence and interest both scored** (1–5 each), placing each stakeholder on the grid. The
  grid drives the engagement approach (manage closely | keep satisfied | keep informed | monitor).
- [ ] **Current sentiment** — champion | supportive | neutral | resistant | hostile — with the date it
  was assessed (`sentiment_assessed`). Sentiment older than ~45 days is **stale** and flagged.
- [ ] **Sentiment is evidenced, not assumed.** Based on an actual interaction, not "they were fine
  last quarter". A guessed sentiment is marked as such.
- [ ] **Engagement strategy present and matched to the grid quadrant.** A high-influence stakeholder
  (manage-closely) with no strategy is a **gap** — the single most important thing to flag.
- [ ] **Comms cadence** set and proportionate to influence/interest — and actually being met.
- [ ] **Key concerns captured** — what this person cares about / fears, so engagement can address it.
- [ ] **Coverage is complete.** No obvious decision-maker, funder, blocker, or affected group missing
  from the register. Silence about a powerful stakeholder is a coverage gap.
- [ ] **Movement is tracked.** Has anyone shifted quadrant or soured since last period? A supportive
  sponsor drifting to neutral is an early-warning signal worth surfacing.
- [ ] **Resistance has a response.** A resistant/hostile high-influence stakeholder has a specific
  engagement action (linked ACT), not just a label.

## 3. Reframe patterns

| Weak form | Why it fails | Strong form |
|---|---|---|
| "Sponsor: supportive." | No date, no evidence, no strategy — probably stale. | "STK-003 Sam Ortiz (sponsor), influence 5 / interest 4 — supportive (assessed 18 Jul, backed the descope at SteerCo). Strategy: weekly 1:1, lead with decisions. Concern: the 14 Aug date." |
| "Finance Director — keep informed." | High influence mislabelled low-touch; no sentiment. | "STK-007 Finance Director, influence 5 / interest 2 — **manage closely** on budget decisions; sentiment neutral (assessed 15 Jul). Strategy: monthly cost brief; escalate any forecast breach early." |
| A powerful regulator absent from the register | Coverage gap — the one who can stop the project isn't tracked. | Add STK entry, score influence 5, assess sentiment, set an engagement strategy and cadence. |
| "Ops Manager — resistant" (label only) | Names the problem, does nothing about it. | "STK-011 Ops Manager, influence 4 — resistant (worried about headcount). Strategy: ACT-120 involve in design workshops, address headcount concern directly — owner PM, due 30 Jul." |

**Fully worked rebuild** — a stale, strategy-less entry on a key stakeholder:

> *As received:* "**Regional Director — supportive.**"
>
> *After the coverage check:* influence 5, but sentiment was last read three months ago, there's no
> engagement strategy, and the last two status packs didn't go to her. She is a manage-closely
> stakeholder being run as monitor. Classic end-of-project-surprise setup.
>
> *Improved record:*
> **STK-005 — Regional Director**
> **Influence:** 5. **Interest:** 3. **Quadrant:** manage closely.
> **Sentiment:** unknown — last assessed 12 Apr (**stale, >45 days**); needs a fresh read.
> **Strategy (gap → filled):** ACT-121 PM to hold a re-alignment 1:1 and re-assess sentiment — due
> 28 Jul. Cadence: fortnightly summary + monthly 1:1. **Key concern:** regional rollout impact on
> her teams.
> **Flag to PM:** high-influence stakeholder with no current sentiment and no engagement plan — this
> is the most likely source of a late surprise.

## 4. When to escalate vs just fix

Under **FULL** coaching the agent maintains the register mechanics and flags gaps inline, graduating
to silent maintenance after ~3 accepted (`wiki/coaching-log.md`).

**Silently fix + note:**
- Derive and set the grid quadrant from influence/interest scores.
- Flag any sentiment older than ~45 days as **stale** and list it for re-assessment.
- Flag high-influence stakeholders with no engagement strategy as **coverage gaps**.
- Surface quadrant drift / souring sentiment period-on-period.
- Prompt for missing key-concern and cadence fields.
- Note obvious missing stakeholders (an unlisted decision-maker or affected group).

**Raise with the PM — do not decide:**
- **Setting or changing an influence, interest, or sentiment rating** — these are assessments the PM
  owns; the agent proposes from evidence and flags staleness, but does not score people for them.
- **Any actual engagement with a stakeholder** — a message, meeting, or comms going *to* a
  stakeholder crosses the "sharing with a stakeholder" gate: draft, don't send.
- **Committing to a stakeholder on the PM's behalf**, or promising an outcome.
- **Judging a stakeholder hostile/resistant** in a way that would be recorded and acted on — confirm
  the read with the PM; labels have consequences.

Rule of thumb: the agent keeps the map *current, complete and honest* and flags the gaps; the PM owns
the ratings, the relationships, and every actual contact.
