# Standard: Action quality

*Applies to `registers/actions/` (ACT). Referenced by the ingest coach step, meeting-minutes
extraction, the weekly stale sweep, and SOUL principle 6.*

## 1. The principle

An action with no owner and no due date is not an action — it is a good intention with a paper trail.
The two fields that make an action real are the two most often missing: **who** and **by when**.
Without an owner, no one does it; without a due date, it can never be late, so it is never chased,
so it never closes. A good action is **closable**: specific enough that anyone can tell whether it's
done. The agent's standing job is to refuse to log intention as action, and to chase what's overdue —
commitments made in meetings must not evaporate.

## 2. The checklist

For every action the agent captures or reviews (ACT):

- [ ] **Named owner** — one specific person, not a team, not "someone", not "we". Shared ownership
  means no ownership; split it into per-owner actions.
- [ ] **Due date** — an absolute date, not "soon", "next sprint", or blank. No date → not yet an
  action; the agent asks.
- [ ] **Closable / verifiable.** Would both parties agree when it's done? "Look into the API" is not
  closable; "confirm the API rate limit with the vendor and record it in RSK-042" is.
- [ ] **Single, concrete deliverable.** One action = one outcome. A multi-part action hides partial
  failure — split it.
- [ ] **Origin recorded** — meeting, chat, ingest, review — so it traces back to where it was
  committed (`origin:`).
- [ ] **Live status** — open | done | overdue | cancelled. Anything past its due date and not done is
  **overdue** and gets chased, not quietly left open.
- [ ] **Closure is evidenced.** `done` carries a one-line closure note (what was delivered), not just
  a flipped flag.
- [ ] **Not a disguised risk/issue/decision.** "Decide the hosting platform" is a *decision* (DEC);
  "the server might fail" is a *risk* (RSK). Actions *do* things; route the others correctly.

## 3. Reframe patterns

| Weak form | Why it fails | Strong form |
|---|---|---|
| "Follow up on testing." | No owner, no date, not closable. | "ACT-101: Priya to confirm UAT environment is available and email the team — due 25 Jul." |
| "Team to review the risks." | Team = no owner; "review" isn't closable. | "ACT-102: Dana to re-score RSK-030 to RSK-034 with the delivery lead and update the register — due 29 Jul." |
| "Sort out the vendor issue ASAP." | "ASAP" is not a date; "sort out" isn't verifiable. | "ACT-103: Sam to escalate ISS-030 to the vendor account exec and secure a remediation date — due 24 Jul." |
| "Chase everyone for updates." | Multi-target, vague, uncloseable. | Split per owner, each with a specific artefact and date. |
| "Decide on the reporting scope." | This is a **decision**, not an action. | Route to DEC; the *action* is "prepare the options paper for that decision — owner, due date". |

**Fully worked rebuild** — a meeting commitment becomes a real action:

> *As received (from minutes):* "John will have a look at the integration problems and get back to
> us."
>
> *After the quality check:* no date; "have a look" and "get back to us" aren't closable; "John who?"
>
> *Improved record:*
> **ACT-108 — Diagnose the nightly interface record-drop and report cause**
> **Owner:** John Mercer. **Due:** 26 Jul 2026. **Origin:** meeting (`raw/sources/meetings/2026-07-19
> integration sync`). **Status:** open.
> **Closable when:** John has identified the cause of the dropped records and posted findings to the
> team, feeding RSK-039.

If John hadn't been asked for a date in the room, the agent flags it: *"ACT-108 has no committed due
date — I've set a provisional 26 Jul; please confirm with John."*

## 4. When to escalate vs just fix

Under **FULL** coaching the agent tightens actions and asks for missing owners/dates inline,
graduating to silent tightening after ~3 accepted (`wiki/coaching-log.md`).

**Silently fix + note:**
- Rewrite a vague action into a closable, single-deliverable form using the source's own words.
- Convert "ASAP/soon/next sprint" into a proposed absolute date and flag it as provisional.
- Split a multi-owner or multi-part action into discrete ones.
- Re-route a disguised risk/issue/decision to the right register (RSK/ISS/DEC) and note it.
- Mark anything past due as **overdue** and list it for chasing.
- Add a closure note prompt to any `done` action that lacks one.

**Raise with the PM — do not decide:**
- **Assigning an owner** the source didn't name — the agent proposes; the person must actually accept
  the action.
- **Setting or moving a due date** that implies a schedule commitment — propose, don't impose.
- **Cancelling or closing an action** on someone's behalf — closure is the owner's/PM's call.
- **Anything where the "action" is really a decision or a risk-acceptance** — that belongs to the
  human via DEC.

Rule of thumb: the agent guarantees every action is *closable, owned and dated*; the human confirms
*who* is committing and *by when*.
