# Standard: Governance pack

*Applies to steering/board packs in `raw/sources/governance/` and `wiki/governance/`, and to the
decisions they carry (DEC). Referenced by the `governance-prep` skill and SOUL principles 9–10.*

## 1. The principle

A steering committee exists to **make the decisions the project cannot make for itself** — releasing
the next tranche of funding, ruling on a tolerance breach, accepting a material risk, and the
continue/pause/stop call. A pack that spends forty minutes walking the board through status they
could have read, and leaves five minutes for the decisions, is **status theatre**. Good governance is
**decision-led**: lead with the decisions the board must make and cannot delegate, give each the
options and evidence to decide well, and let status be context, not the main event. The **sponsor is
accountable for outcomes and benefits** — not the PM — and board members need genuine delegated
authority, or the meeting is a briefing pretending to be a decision forum.

## 2. The checklist

For a governance pack the agent prepares or reviews:

- [ ] **Decisions up front.** The pack opens with the decisions required this session, each stated as
  a decision — not buried in a status narrative.
- [ ] **Each decision is board-grade.** It's genuinely one the board must make and cannot delegate:
  funding release, tolerance breach, material risk acceptance, scope change, continue/stop. Anything
  the PM can decide shouldn't be taking board time.
- [ ] **Each decision carries options + a recommendation.** Real alternatives, the trade-off, and a
  clear recommended option with rationale (see `decision-hygiene.md`). A single-option "decision" is
  a rubber stamp.
- [ ] **Evidence, not assertion.** Status and RAG in the pack meet `rag-evidence.md` — every colour
  backed by observable data; no watermelons carried into the board.
- [ ] **Tolerance breaches surfaced explicitly.** Anything beyond the delegated tolerances (cost,
  schedule, scope, quality) is named as an escalation, with the decision it forces.
- [ ] **Material risks the board must accept are flagged.** Live severe risks needing a
  risk-acceptance decision are on the agenda, not hidden in an appendix.
- [ ] **Accountability is right.** The pack frames the sponsor as accountable for outcomes/benefits;
  it doesn't quietly park delivery accountability on the PM alone.
- [ ] **Deciders have authority.** The people being asked to decide actually hold the delegated
  authority; if not, the pack routes it to whoever does.
- [ ] **Asks are specific and closable.** Each escalation says what is needed, from whom, by when.
- [ ] **Ruthless on length.** Status is trimmed to what informs the decisions; the pack is a
  decision instrument, not a project diary.

## 3. Reframe patterns

| Weak form | Why it fails | Strong form |
|---|---|---|
| Agenda: "1. Status. 2. Workstream updates. 3. Risks. 4. AOB." | Status theatre — no decision on the agenda. | "1. **Decisions required:** (a) release Phase-2 funding, (b) accept RSK-042 or fund failover, (c) approve 14 Aug date. 2. Evidence behind each. 3. Status for awareness. 4. AOB." |
| "Risks: see appendix." | Buries the risk the board must actually rule on. | "Decision 2: RSK-042 (server failover, P16) — accept the exposure, or approve $40k for a standby node. Recommendation: fund; rationale below." |
| "We recommend continuing." (no alternative) | Continue-only is a rubber stamp, not a gate. | "Gate decision: continue | pause to re-baseline | stop. Recommendation: continue with the revised 14 Aug date. Consequence of each option below." |
| "Budget is tracking." | Unevidenced; hides a tolerance question. | "Budget: forecast $1.29M vs $1.2M baseline — a $90k (7.5%) breach of the 5% tolerance. **Decision:** approve the increased budget or descope. (See `rag-evidence.md`.)" |

**Fully worked rebuild** — a status-led pack becomes decision-led:

> *As received:* a 30-slide deck: 22 slides of workstream status, 3 of risks, a closing "next steps"
> slide, no decisions named.
>
> *After the governance check:* the board is being asked to *absorb* status, not *decide* anything —
> yet buried in the deck are a 7.5% budget breach, an unmitigated P16 risk, and a slipped go-live
> that needs re-baselining. Three board-grade decisions are hidden inside a briefing.
>
> *Improved pack (front page):*
> **SteerCo 25 Jul — Decisions required (3):**
> 1. **Budget tolerance breach.** Forecast $1.29M vs $1.2M baseline (+7.5%, tolerance 5%). Options:
>    approve increase | descope reporting to Phase 2 | hold. *Rec: descope (DEC to be recorded).*
> 2. **Accept RSK-042 or fund mitigation.** P16 server-failover risk. Options: fund $40k standby |
>    formally accept the exposure. *Rec: fund.*
> 3. **Re-baseline go-live to 14 Aug.** Options: approve new date | add a tester to protect 30 Jun |
>    stop. *Rec: approve 14 Aug.*
> **Sponsor (Sam Ortiz) accountable for the benefit case throughout.** Status follows for context
> only. Evidence for each decision on the linked page. *(The agent drafts this; Sam owns and tables it.)*

## 4. When to escalate vs just fix

Governance packs are, by definition, near the accountability line — most of the agent's value here is
*preparation*, and almost everything final is the human's. Under **FULL** coaching the agent
restructures drafts and flags theatre inline, graduating after ~3 accepted (`wiki/coaching-log.md`).

**Silently fix + note (on a draft, before it goes anywhere):**
- Reorder a status-led draft into decision-led form; pull hidden decisions to the front.
- Apply `rag-evidence.md` to every colour in the pack; flag watermelons before the board sees them.
- Surface tolerance breaches and material risks that need a board ruling as explicit agenda decisions.
- Attach options + recommendation to each decision per `decision-hygiene.md`.
- Trim status that doesn't inform a decision.
- Flag where the pack misplaces accountability (PM carrying what the sponsor owns).

**Raise with the PM — do not decide (and never send):**
- **Tabling or sending the pack** — anything going to the board crosses the "sharing with a
  stakeholder" gate: draft, the PM/sponsor tables it.
- **The recommendation on any decision** — the agent may *recommend* with evidence, but funding
  release, tolerance breaches, risk acceptance, scope, and continue/stop are the board's to make and
  the sponsor's to own.
- **Framing something as a tolerance breach or escalation** where the tolerance itself is a judgment
  call — confirm the threshold with the PM.
- **Recording the board's decisions** — capture them as DEC only after the human confirms the outcome.

Rule of thumb: the agent builds a pack that lets the board *decide well* — decisions first, evidence
attached, theatre removed; the human tables it, and the board (with the sponsor accountable) decides.
