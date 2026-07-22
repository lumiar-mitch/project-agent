---
name: risk-register-review
description: Use this to "review my risk register", red-team the risks, or automatically whenever a risk register is ingested. Assesses the whole register against standards/risk-quality.md — cause/risk/effect confusion, issues masquerading as risks, missing owners/mitigations/review dates, duplicates, stale entries, and optimism — and proposes reframes without ever silently changing a rating.
---

# Risk register review

The red-teamer for risks. You assess the entire register against `standards/risk-quality.md`,
propose stronger versions, and apply fixes per the coaching posture. You never set or change a
probability, impact, severity, or response — those are the human's ratings to own.

## Before you start

1. Read `standards/risk-quality.md` — it is the rubric for everything below.
2. Load every item in `registers/risks/` (or, if a register was just ingested, the newly extracted
   set plus the existing open items for context).
3. Read `views/raid.md` and PROJECT.md for the project's objectives — a risk is only assessable
   against what it threatens.

## Assess each risk against the standard

For every risk, check:

1. **Cause → risk → effect.** Is it a proper conditional statement — "because <fact/cause>,
   <uncertain event> may occur, leading to <effect on objectives>"? Flag risks that are stated as a
   bare fact, a cause with no event, or an effect with no event. Propose the reframed statement.
2. **Issue masquerading as a risk.** Has the "risk" already happened, or is it a certainty? If so it
   is an **issue** — propose moving it to `registers/issues/` (`from_risk`) and say why.
3. **Missing owner.** Owner must be a **named person, never a team**. Flag blanks and team-owners.
4. **Missing mitigation / response.** Is there a `response` (avoid|reduce|transfer|accept) and at
   least one linked mitigating action? Flag risks with no plan.
5. **Missing or stale review date.** `review` is mandatory. Flag missing dates and any review date
   in the past.
6. **Duplicates.** Flag risks that describe the same underlying uncertainty; propose a merge
   (keeping the fuller History).
7. **Optimism / under-scoring.** Note single-point confidence, suspiciously low probabilities on
   material threats, and severity that looks softened. Per `standards/rag-evidence.md`, scepticism
   here is realism — but you *propose*, you do not re-rate.

## Output findings + proposed reframes

Produce a table or list: for each flagged risk, the ID, the problem (which check failed), and the
proposed stronger version (reframed statement, suggested owner, missing fields to fill, or
merge/move recommendation).

## Apply per the coaching posture

- Write the improved **statement, structure, and missing non-rating fields** into the register item.
  Fix cause→risk→effect wording, add the mitigation link stubs, propose the review date.
- **Never silently change a rating.** Probability, impact, severity and response acceptance stay as
  found; surface your proposed values and let the human set them. `severity` is P×I and
  agent-maintained *once the human sets P and I*.
- Reframing a risk to an issue, or merging duplicates, is a structural change — propose it and make
  the move only with the human's nod (it removes something they created).
- Per coaching mode (default **full**): give before/after/why with a pointer to
  `standards/risk-quality.md`; graduate to silent after ~3 accepted lessons of the same kind.

## Finish

1. If invoked standalone, refresh `views/raid.md` and `STATE.md` after any applied structural fixes.
2. Append `wiki/coaching-log.md` with the *patterns* found (e.g. "half the register states effects,
   not events").
3. Append `wiki/log.md`: `## [YYYY-MM-DD] review | Risk register review` with the count assessed,
   flagged, and reframed.
4. Report to the PM: the findings list, the proposed reframes, and the ratings you are asking them
   to set or confirm. The register is stronger; the judgment calls are still theirs.
