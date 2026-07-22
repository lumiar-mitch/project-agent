# Standard: RAG evidence (anti-watermelon)

*Applies to any status claim — `STATE.md`, status reports, governance packs, workstream summaries.
Referenced by the `status-drift` skill, the weekly review, and SOUL principles 1–2 and 8.*

## 1. The principle

A RAG colour is a **claim, not a status**. Green does not mean "green" — it means someone is
*asserting* green, and the only question that matters is what observable evidence backs the
assertion. Without data you are just another person with an opinion. The classic failure is the
**watermelon**: green on the outside, red on the inside — a report that stays green while the
schedule slips, severe risks sit open, and estimates never move, right up until the surprise. The
agent's job is to make the inside visible. And it must protect the meaning of red: **red is a
request for support, not a confession of failure**. If red gets punished, reporting goes green and
governance goes blind.

## 2. The checklist

For every RAG colour the agent finds or is asked to produce:

- [ ] **Evidence attached.** Is there an *observable* basis — a completed deliverable, a measured
  metric, a passed milestone, actuals vs baseline? "On track" is not evidence; "3 of 4 milestones
  met, CPI 0.98" is.
- [ ] **Colour matches the evidence.** Does the evidence actually support the colour, or is it green
  by habit? A green with no supporting data is **unverified** and flagged as such.
- [ ] **No schedule slip hiding behind green.** Compare forecast dates to baseline. Movement to the
  right under a green is the number-one watermelon tell.
- [ ] **No severe open risks/issues under "on track".** Cross-check the register: an open P16 risk or
  a high-priority issue is incompatible with an unqualified green.
- [ ] **Estimates are moving.** A % complete or ETC that is identical to last period, week after
  week, is a smell (the "90% done for three months" pattern).
- [ ] **Trend, not just point.** Is this better or worse than last period? A green that was amber
  last week for a still-unresolved reason is really amber.
- [ ] **Red is framed as a support request.** Does a red/amber say what help is needed and from
  whom? A colour with no ask is theatre.
- [ ] **The colour is at the right granularity.** An overall green that averages away a red
  workstream is hiding it — surface the component.

## 3. Reframe patterns

| Weak form | Why it fails | Strong form |
|---|---|---|
| "Delivery: 🟢 On track" | A claim with no evidence and no trend. | "Delivery: 🟢 — 3 of 4 Sprint-12 stories accepted, CPI 0.98, no milestone movement this period (evidence: `raw/sources/reports/2026-07-15 burndown`)." |
| "🟢 Overall — minor issues only" while RSK-042 (P16) is open | Green contradicts the register. | "🟠 Overall — on scope and cost, but RSK-042 (server failover, P16) remains open and unmitigated; see ask below." |
| "Schedule 🟢" with go-live moved 30 Jun → 14 Aug | Slip hidden behind green. | "🔴 Schedule — go-live has moved from 30 Jun to 14 Aug (6-week slip) driven by UAT resourcing; **ask:** approve one additional tester or accept the new date (decision for SteerCo)." |
| "Build 🟢 — 90% complete" (same as last 3 reports) | Frozen estimate; % complete not moving. | "🟠 Build — reported 90% for three periods; remaining 10% is the reporting module, now understood to be ~4 weeks. Revised ETC 28 Aug." |

**Fully worked rebuild** — a status line that reads green but isn't:

> *As received:* "**Payments workstream: 🟢 Green — progressing well.**"
>
> *After the evidence check:* the register shows ISS-030 (gateway certification blocked) open and
> high-priority, and the milestone "PCI sign-off" has slipped from 10 Jul to a date that is now
> TBC. The green is a watermelon.
>
> *Improved claim:* "**Payments: 🔴 Red** — certification (ISS-030) has been blocked on the vendor
> for 3 weeks; the PCI sign-off milestone has slipped from 10 Jul with no new date. This is not
> deteriorating quietly — it needs escalation. **Ask:** sponsor to raise with vendor exec by 25 Jul,
> or we hold the go/no-go. Evidence: `raw/sources/meetings/2026-07-18 payments standup`."

Red here is doing its job: naming the blocker, quantifying the slip, and carrying a specific ask.

## 4. When to escalate vs just fix

Under **FULL** coaching, the agent attaches evidence and flags mismatches inline, then graduates to
silent annotation once the PM has accepted the pattern ~3 times (`wiki/coaching-log.md`).

**Silently fix + note:**
- Attach the supporting evidence (or mark "**unverified — no evidence in sources**") to any colour.
- Surface a register contradiction next to the claim (open severe risk under a green).
- Flag a frozen estimate or a rightward schedule slip hiding under green.
- Add the missing trend ("amber last period, still unresolved").

**Raise with the PM — do not decide:**
- **Changing a reported RAG colour.** The agent presents the evidence and *recommends* a colour; the
  PM owns what the dashboard says. The agent never silently repaints a status the PM will send.
- **Anything that becomes an external report or pack** — that crosses the "sharing with a
  stakeholder" gate; draft, don't send.
- **Deciding an escalation is warranted** — the agent frames the ask; the PM chooses to escalate.
- **Softening a red.** The agent must never do this at all — it is a hard rule, not a coaching call.

Rule of thumb: the agent guarantees the colour is *honest and evidenced*; the PM owns what colour is
*published* and who it goes to.
