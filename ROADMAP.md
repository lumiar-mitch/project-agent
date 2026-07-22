# Roadmap

This is the provocation more than a plan — a sketch of where a project agent could go, so
you can imagine what AI on a project looks like *beyond* "fix up my status report". None of what
follows is built yet.

**v1 is deliberately local-first.** Your project lives in a folder on your machine, the install has
zero auth, and nothing connects to an internal system. That is a design choice, not a gap: it makes
the kit genuinely turnkey, keeps a clean local-first posture (your files live only in your folder, with
no third-party store beyond Claude itself), and removes the biggest
setup barrier. Everything below trades some of that simplicity for reach, and only earns its place
if it holds the line on trust, citations and the accountability boundary.

## Where this could go (not yet built)

### SharePoint / Teams connectors

Most project documents live in SharePoint and most conversations happen in Teams. A connector would
let the brain read from where your project already is, instead of you dropping files into `raw/inbox/`.
Held back from v1 on purpose: a live connector needs an MCP server *and* a Microsoft sign-in that
cannot be automated, and it opens a corporate-infosec conversation. Doing it well — read-only,
scoped, transparent about what it touched — is the first big step up from local-first.

### A long-running "watch and brief me" mode

Instead of you asking "what changed this week?", the brain runs continuously in the background:
watching the sources it can see, noticing when a new risk appears without an owner or a status flips
green with no evidence, and briefing you proactively — *"three things moved since yesterday, one of
them needs you before Thursday"*. Project Agent becomes an ambient team member rather than a tool
you open.

### Drift tracking across a project's full history

Registers as one-file-per-item already give a clean git history. This turns that history into
insight: how has this risk's severity moved over the last quarter? How many times has this decision
been re-litigated? Is this workstream's RAG quietly amber-creeping while the narrative stays
positive? Drift tracking makes the *shape* of a project over time visible — the thing status reports
systematically hide.

### A community skill marketplace

The kit is a platform that grows in your hands — ask it, and it writes you a new skill. The next
step is sharing: a place where PMs publish the skills and standards they have built (a better
governance-pack check, a domain-specific risk taxonomy, a delivery-methodology-aware review) and
fork each other's. The moat of this whole project is encoded judgment; a marketplace lets that
judgment compound across a community instead of sitting in one person's fork.

---

Have a strong opinion about what should come next, or built a skill worth sharing? That is the point.
Open an issue or send a pull request.
