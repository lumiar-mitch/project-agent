# Standard: Meeting minutes

*Applies to `raw/sources/meetings/` on ingest and to the extraction into `registers/`. Referenced by
the ingest pipeline, the `ingest` skill, and — through what it feeds — every other standard.*

## 1. The principle

Minutes are not a transcript; they are the project's **extraction surface**. Good minutes exist so
that decisions, actions, and risks/issues can be pulled out cleanly — a commitment spoken in a
meeting is an **action**, and if it isn't captured with an owner and a due date, it evaporates the
moment the call ends. The test of a set of minutes is not "does it read well" but "can I extract every
decision, every owned-and-dated action, and every new risk or issue from it, unambiguously". This
standard is the front door: it feeds `decision-hygiene.md`, `action-quality.md`, and
`risk-quality.md`, and applies each of them to what the meeting produced.

## 2. The checklist

When ingesting minutes or a transcript, the agent extracts and tests:

- [ ] **Every decision captured as a DEC** — meeting `decision-hygiene.md`: options, decider, forum,
  date, what it resolves. "It was agreed…" gets a named decider or it's flagged.
- [ ] **Every commitment captured as an ACT** — meeting `action-quality.md`: named owner + absolute
  due date + closable. "John will look into it" is chased for an owner and a date, not logged as-is.
- [ ] **Every new risk/issue captured** — via `risk-quality.md`: is it uncertain (RSK) or already
  happened (ISS)? rebuilt into cause → risk → effect.
- [ ] **Nothing dropped between what was said and what was recorded.** Commitments, concerns raised,
  and dates mentioned all land somewhere in a register — or are explicitly noted as not actionable.
- [ ] **Attribution is clear.** Who said/owns/decided what — no floating "we", "someone", "the team".
- [ ] **Absolute dates.** "By next Friday" is converted to the calendar date; "last week" to the date.
- [ ] **Deduped against open items.** New actions/risks/decisions are checked against the existing
  registers before creating — update the open item, don't spawn a duplicate.
- [ ] **RAG claims from the meeting get the evidence test** (`rag-evidence.md`) — a verbal "we're
  green" isn't logged as green without a basis.
- [ ] **Source filed and cited.** The raw minute is moved to `raw/sources/meetings/` *before* any
  citation, so register links point at the permanent location; every extracted item cites it with an
  absolute date.
- [ ] **Ambiguity surfaced, not smoothed.** Where the minutes are unclear on owner/date/decision, the
  agent flags the gap to the PM rather than inventing a plausible fill.

## 3. Reframe patterns

| Weak minute line | What it really is | Extracted to |
|---|---|---|
| "We discussed the vendor and agreed to stick with them." | A decision, missing options/decider. | DEC (see worked example) — flagged for decider + options. |
| "John will have a look and get back to us." | A commitment = an action, no owner-surname/date. | ACT-108, owner John Mercer, provisional due date flagged for confirmation. |
| "There's a concern the server could fail during billing." | A new risk. | RSK-042, rebuilt into cause → risk → effect. |
| "The gateway cert is blocked — has been for weeks." | Already happened = an issue. | ISS-030, priority + owner + target date. |
| "Sarah's happy with progress." | An unevidenced status/sentiment claim. | Note against STK; not logged as 'green' without a basis. |
| "Aim to finish by next Friday." | A date reference. | Converted to the absolute date on the relevant ACT. |

**Fully worked example** — one paragraph of minutes, fully extracted:

> *Raw minute:* "Team ran through the integration issues. John will look into the dropped records.
> We agreed to stay with Vendor A rather than re-tender, given the timeline. There's a worry the
> billing server has no failover. Aim to have the standby sorted before the next billing run."
>
> *Extraction (each item filed, source cited to `raw/sources/meetings/2026-07-19 integration sync`):*
> - **DEC-019** — Retain Vendor A (do not re-tender). Options: retain | re-tender | in-house. Decided
>   by [**flag: who chaired? confirm decider**], 19 Jul. Resolves the open question behind RSK-042.
> - **ACT-108** — John Mercer to diagnose the dropped-records cause and report to the team. Due
>   26 Jul (**provisional — no date committed in the room; confirm with John**). Origin: meeting.
> - **RSK-042** — *Because* the billing server has no failover (fact), *it may be unavailable* during
>   the month-end run (uncertain), *leading to* missed billing SLAs (effect). Owner [**flag: unassigned
>   — propose Priya, confirm**].
> - **ACT-109** — Stand up the standby node before the next billing run (i.e. before 31 Jul). Owner
>   [**confirm**]. Origin: meeting. (Mitigation linked to RSK-042.)
>
> Two flags go back to the PM in the ingest report: DEC-019 needs a named decider, and RSK-042 /
> ACT-109 need an owner. Everything else is filed.

## 4. When to escalate vs just fix

Under **FULL** coaching the agent extracts, structures, and flags gaps in the ingest report,
graduating to silent extraction of the routine cases after ~3 accepted (`wiki/coaching-log.md`).

**Silently fix + note:**
- Extract decisions, actions, and risks/issues into the registers, each shaped to its own standard.
- Convert relative dates to absolute; attribute "we/someone" to a named person where the source makes
  it unambiguous.
- Dedupe against open items and update rather than duplicate.
- File and cite the source correctly (move to `raw/sources/meetings/` before citing).
- List every gap (missing owner, missing date, unnamed decider, unevidenced RAG) in the report.

**Raise with the PM — do not decide:**
- **Any decision the minutes imply** — the agent captures what was decided; it never decides, and it
  confirms an ambiguous decider rather than guessing.
- **Assigning owners or setting due dates** the meeting didn't nail down — propose, confirm, don't
  invent. An invented owner is a fabrication.
- **Anything the extraction routes to risk acceptance, scope, ratings, or a decision** — those inherit
  the accountability line from their own standards.
- **Filling a genuine ambiguity.** If it's unclear whether something was decided or merely discussed,
  the agent asks. It never smooths an ambiguous minute into a false certainty (SOUL principle 4).

Rule of thumb: the agent guarantees *nothing said is lost* — every decision, action and risk is
extracted and shaped to standard; the human confirms the owners, dates, and decisions the room left
loose.
