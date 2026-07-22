# Standard: Risk quality

*Applies to `registers/risks/` (RSK) and, by exclusion, `registers/issues/` (ISS).
Referenced by the ingest coach step, the `risk-register-review` skill, and SOUL principle 5.*

## 1. The principle

A risk register is where projects go to lie to themselves. Most "risks" on most registers
are not risks at all — they are facts, worries, or things that have already gone wrong dressed
up in risk language. A genuine risk is **uncertain** and would **affect an objective**: if it is
certain it is a constraint or a fact; if it has already happened it is an **issue**; if it can't
touch an objective it is noise. The single most valuable thing this agent does to a register is
force the discipline of **cause → risk event → effect**, because that structure is what separates
the three things everyone confuses. We counter optimism bias by default: a thin, cheerful register
is a warning sign, not a clean bill of health.

## 2. The checklist

The agent applies these tests to every risk on ingest and in review:

- [ ] **Uncertain, not certain.** Is the event genuinely in doubt? If it *will* happen, it's a
  constraint/fact. If it *has* happened, it's an **issue** (reframe → ISS, tell the PM why).
- [ ] **Cause → risk → effect present.** The body reads "**Because** <cause/fact that is true today>,
  <**uncertain event**> may occur, **leading to** <effect on a named objective — cost, schedule,
  scope, quality, benefit>." All three parts, none collapsed into another.
- [ ] **Not a cause masquerading as a risk.** "Because we have no test environment" is a cause, not
  a risk. The risk is what that cause makes uncertain.
- [ ] **Not an effect masquerading as a risk.** "The project will be late" is an effect. The risk is
  the uncertain event that would cause lateness.
- [ ] **Named owner.** A specific person, never a team, a role-in-the-abstract, or "TBC". The owner
  is who manages the response, not who's to blame.
- [ ] **Probability and impact both scored** (1–5 each), with severity = P × I maintained by the agent.
- [ ] **At least one mitigation, and each mitigation is itself an action** with an owner and a due
  date (linked ACT). A mitigation with no owner/date is a wish.
- [ ] **A response type** chosen deliberately: avoid | reduce | transfer | accept. "Accept" is a
  decision, not a default — see escalation below.
- [ ] **A live review date** (`review:`) in the future. A risk no one has looked at in months is
  either dead or realising quietly.
- [ ] **Distinct from siblings.** Not a duplicate of an open risk; not five variants of one risk.
- [ ] **Proportionate scepticism.** If a whole workstream has no risks, or every risk is low/low,
  the agent flags the *absence* — optimism bias, not safety.

## 3. Reframe patterns

| Weak form | Why it fails | Strong form |
|---|---|---|
| "Risk: the vendor might be late." | Bald event, no cause, no effect, no owner. | See worked example below. |
| "Risk: we don't have enough testers." | This is a **cause** (a fact true today), not an uncertain event. | "Because the test team is one FTE short (fact), UAT may not complete within the two-week window (uncertain), delaying go-live past 30 Sept (effect)." |
| "Risk: the project could go over budget." | This is an **effect**. Every risk could cause it; it names none. | "Because the scope for the reporting module is still unbaselined, additional build effort may be required, leading to a forecast overrun against the $1.2M budget." |
| "Risk: the server went down last week." | Already happened → it's an **issue**, not a risk. | Reframe to ISS-###; if recurrence is uncertain, *also* raise a forward risk about the next outage. |
| "Risk: integration is hard." | A worry, not an event; nothing testable, no owner. | "Because the two systems use incompatible date formats (fact), the nightly interface may drop records (uncertain), leading to inaccurate month-end reporting (effect)." |

**Fully worked rebuild** — "Risk: the server might go down":

> **RSK-042 — Primary application server outage during peak billing**
> **Statement:** *Because* the production server is a single node with no failover configured
> (cause — true today), *the application may become unavailable* during the month-end billing run
> (uncertain event), *leading to* missed billing SLAs and up to two days of delayed revenue
> recognition (effect on the cost and reputation objectives).
> **Owner:** Priya Nair (infra lead). **Probability:** 3. **Impact:** 4. **Severity:** 12.
> **Response:** reduce. **Mitigations:** ACT-118 stand up warm standby node (owner Priya, due 15 Aug);
> ACT-119 rehearse failover before the Sept run (owner Priya, due 22 Aug).
> **Review:** 05 Aug.

Note what changed: a vague noun became a *conditional event*; the cause is a verifiable present
fact; the effect names the objective and quantifies it; there is an owner, a score, mitigations that
are real actions, and a review date.

## 4. When to escalate vs just fix

Under **FULL** coaching the agent corrects first and explains briefly (before/after + a pointer to
this standard), tracked in `wiki/coaching-log.md`. After ~3 accepted corrections of the same pattern
it applies the fix silently and reports the pattern in the weekly digest.

**Silently fix + note** (mechanical quality, no judgment call):
- Rewrite a weak statement into cause → risk → effect form using facts already in the source.
- Recompute and maintain severity (P × I).
- Convert an already-happened "risk" into an **issue** (ISS), and note the reframe.
- Chase a missing review date forward to a sensible default and flag it as provisional.
- Flag duplicates and propose a merge.

**Raise with the PM — do not decide (the accountability line):**
- **Any probability or impact rating**, or a change to one. Ratings are the PM's call; the agent
  proposes and evidences, never sets.
- **Choosing or recording `response: accept`** — accepting a live risk is a governance act; surface
  it, frame the exposure, let the human own it (and usually record a DEC).
- **Assigning or changing an owner** — the agent proposes a candidate; the person must actually
  agree to own it.
- **Closing a risk**, or judging it no longer credible.
- **Anything that implies scope, cost, or schedule tolerance has moved.**

Rule of thumb: the agent may make a bad risk into a *good* risk; only the PM may decide *how big* it
is, *who* owns it, whether to *accept* it, or when to *close* it.
