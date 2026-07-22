# Standard: Decision hygiene

*Applies to `registers/decisions/` (DEC). Referenced by the ingest coach step, the `governance-prep`
skill, meeting-minutes extraction, and SOUL principles 9–10.*

## 1. The principle

A decision that records only the outcome is a rubber stamp, not a decision. The value of a decision
log is not "what we chose" — it's **what we chose it over, who chose it, and why**, so that six
months later no one relitigates it and everyone can see the reasoning held. A "decision" with a
single option was never a decision; it was a foregone conclusion someone wanted minuted. Good
governance is **decision-led**: the register captures the options considered, the person accountable,
the forum, the date, and exactly what the decision resolves. If the agent can't extract those, it
hasn't found a decision — it's found a status update wearing a decision's clothes.

## 2. The checklist

For every decision the agent records or reviews (DEC):

- [ ] **Options considered — plural.** At least two genuine options are named. A one-option record is
  flagged: either surface the alternatives that were weighed, or mark it as a *ratification*, not a
  decision.
- [ ] **Decider named.** A specific person or a named forum with the authority to make it — not "the
  team", not passive voice ("it was decided").
- [ ] **Forum + date.** Where and when (SteerCo / sponsor / working group), with an absolute date.
- [ ] **What it resolves.** The decision links to the risk, issue, option, or requirement it settles
  (`resolves[]`). A decision that resolves nothing is orphaned — why was it made?
- [ ] **Rationale.** One or two lines on *why this over the others* — the trade-off accepted.
- [ ] **Authority to decide.** Did the decider actually hold delegated authority for this? A decision
  above someone's tolerance is really an escalation.
- [ ] **Status is honest.** proposed | pending | decided | superseded. A `decided` decision is
  immutable — it changes only by a *superseding* decision, never by silent edit.
- [ ] **Decision-led, not status-led.** The record leads with the choice, not with narrative. If it
  reads like a paragraph of context with a choice buried in it, restructure it.

## 3. Reframe patterns

| Weak form | Why it fails | Strong form |
|---|---|---|
| "Decided to use AWS." | One option, no decider, no forum, no rationale. | "DEC-011: adopt AWS for hosting. Options considered: AWS, Azure, on-prem. Decided by Sam Ortiz (sponsor) at SteerCo 12 Jul. Rationale: existing enterprise agreement + team skills; on-prem rejected on lead time. Resolves RSK-030 (hosting uncertainty)." |
| "It was agreed to descope reporting." | Passive voice, no accountable person, no alternative weighed. | "DEC-014: defer the reporting module to Phase 2. Options: build now (blows 14 Aug date), descope to Phase 2, add contractor. Decided by Sam Ortiz at SteerCo 18 Jul over the delivery lead's build-now preference. Resolves the schedule pressure in RSK-041." |
| "Going with option B (per the deck)." | Rationale and alternatives live in a slide, not the record; unfindable later. | Pull the options, decider and rationale *into* the DEC body; cite the deck as the source. |
| A 'decision' to "continue the project" with no options | Continue/stop with only one option is theatre. | Frame as a genuine gate: continue | pause | stop, each with its consequence, decided by the board. |

**Fully worked rebuild** — a meeting minute line becomes a proper decision:

> *As received (minute):* "We talked through the vendor situation and decided to stick with
> Vendor A for now."
>
> *After the hygiene check:* who is "we"? what were the options? what does it resolve? why?
>
> *Improved record:*
> **DEC-019 — Retain Vendor A for the integration build (do not re-tender)**
> **Options considered:** (a) retain Vendor A; (b) re-tender the build; (c) bring in-house.
> **Decided by:** Sam Ortiz (sponsor), SteerCo, 18 Jul 2026.
> **Rationale:** re-tendering adds ~8 weeks and breaches the go-live tolerance; Vendor A's recent
> delays are being managed under RSK-042. In-house rejected — no capacity.
> **Resolves:** the open question behind RSK-042; supersedes nothing.
> **Status:** decided (immutable — change only via a superseding DEC).
> *(Source: `raw/sources/meetings/2026-07-18 steerco`.)*

## 4. When to escalate vs just fix

Under **FULL** coaching the agent structures the record and asks for the missing pieces inline,
graduating to silent structuring after ~3 accepted (`wiki/coaching-log.md`).

**Silently fix + note:**
- Restructure a buried decision into decision-led form (choice first, then options, decider, forum,
  date, rationale, resolves).
- Flag a one-option "decision" and ask what alternatives were weighed, or relabel it a ratification.
- Rewrite passive "it was decided" into the named decider once the source makes them identifiable.
- Link `resolves[]` to the register items the decision settles.
- Mark a `decided` record immutable and route any later change through a superseding DEC.

**Raise with the PM — do not decide:**
- **Recording the decision itself**, or its outcome. The agent never makes or changes the substance
  of a decision; it captures and structures what the human/forum decided.
- **Superseding or reopening a `decided` decision** — needs the PM's explicit act and a new DEC.
- **Any decision touching scope, funding, risk acceptance, or a tolerance breach** — these are the
  board's/sponsor's to make; the agent frames the options and evidence (see `governance-pack.md`) and
  stops at the accountability line.
- **Attributing a decision to a person** when the source is ambiguous about who actually decided —
  confirm, don't guess.

Rule of thumb: the agent guarantees a decision is *well-recorded* — options, decider, forum, date,
rationale; only the human makes, changes, or supersedes the decision itself.
