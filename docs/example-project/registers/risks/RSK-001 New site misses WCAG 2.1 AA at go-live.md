---
id: RSK-001
title: New site misses WCAG 2.1 AA at go-live
type: threat
status: open
owner: Leah Consadine
raised_by: Dana Okafor
raised: 2026-05-14
review: 2026-06-11
probability: 3
impact: 4
severity: 12 (high)
proximity: 2026-11-06
response: reduce
workstream: Accessibility
links: [ACT-001, DEC-001]
updated: 2026-05-16
---

# RSK-001 — New site misses WCAG 2.1 AA at go-live

## Cause → risk → effect

Because the top-tasks forms and migrated content are being built by multiple authors on a compressed
schedule and accessibility has historically been checked late, **the new site may not fully meet WCAG
2.1 AA by go-live**, leading to a non-compliant public service, reputational exposure for the
council, and potential remediation cost and delay after launch.

## Assessment

- **Probability 3 / Impact 4 → severity 12.** Impact is high because accessibility compliance is a
  legal and reputational obligation for a government site, not a nice-to-have.
- **Proximity:** the accessibility audit is booked for 2026-11-06, three weeks before go-live —
  little runway to fix findings, which is what makes proximity bite.
- **Response: reduce.** Bring accessibility checks forward into each sprint rather than a single
  audit at the end.

## Mitigations

- [ACT-001] — Embed accessibility acceptance criteria into the definition of done for every form and
  template (owner: Leah Consadine, due 2026-05-28).
- Interim accessibility spot-check at design sign-off (2026-07-10), not only at the final audit.

## History

- **2026-05-14** — Raised at kickoff by Dana Okafor; owner assigned to the external accessibility
  advisor rather than "the team". ([source](../../raw/sources/meetings/2026-05-14%20Kickoff.md))
- **2026-05-16** — Severity set 12; mitigation ACT-001 created.
