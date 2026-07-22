---
id: DEC-001
title: Adopt the Northbank CMS on the council cloud tenancy
status: decided
decided_by: Priya Menon
forum: Project Steering Committee
date: 2026-05-14
resolves: []
supersedes: null
review: null
workstream: Platform
links: [RSK-001]
updated: 2026-05-14
---

# DEC-001 — Adopt the Northbank CMS on the council cloud tenancy

## Decision

The project will build the new website on the Northbank CMS, hosted within the council's existing
approved cloud tenancy, rather than a separate SaaS platform or an open-source CMS self-hosted by IT.

Decided by Priya Menon (sponsor) at the Steering Committee on 2026-05-14.

## Options considered

1. **Northbank CMS on the council cloud tenancy** *(chosen)* — uses the delivery partner's supported
   product inside infrastructure IT already governs. Fastest to stand up, no new vendor security
   assessment, aligns with the council's cloud-first policy. Trade-off: some lock-in to Northbank's
   product.
2. **A separate SaaS CMS** — richer out-of-the-box features, but triggers a full vendor security and
   data-residency assessment (6–8 weeks) the schedule cannot absorb, and puts resident data outside
   the council tenancy.
3. **Open-source CMS self-hosted by council IT** — no licence cost and no lock-in, but IT does not
   have capacity to run it and the operating burden falls on a team already stretched. Rejected on
   supportability.

## Rationale

Option 1 best balances speed, supportability and the council's existing security posture. The
lock-in trade-off is accepted as manageable given the content is portable and the migration approach
keeps pages as structured content.

## History

- **2026-05-14** — Decided at Steering Committee.
  ([source](../../raw/sources/meetings/2026-05-14%20Kickoff.md))
