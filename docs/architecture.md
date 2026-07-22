# Architecture

This explains how a Project Agent instance is put together and why. It is for the curious and for
contributors — you do not need to read it to use the tool. If you just want to run one, start with
[GETTING-STARTED.md](../GETTING-STARTED.md).

## The idea in one line

Take the [Karpathy LLM-wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
— an agent that maintains a wiki about a body of knowledge — specialise it for a single project, and
add a structured register layer so that lifecycle data (a risk, a decision) lives as data, not prose.
Then wire good practice through the whole thing so it teaches while it works.

## The four-layer model

```
raw/        immutable facts — every document, exactly as received; never edited
  → registers/   structured truth — one file per item: an ID, an owner, a lifecycle
  → wiki/        narrative truth — what it means and how it connects; links to register IDs
  → views/ + STATE.md   derived dashboards — regenerated from registers; never hand-edited
```

Each layer has one job, and information flows one way: facts arrive in `raw/`, get distilled into
`registers/` and explained in `wiki/`, and are rolled up into `views/`. Nothing downstream is ever
the source of truth for something upstream.

### Layer 1 — `raw/` (immutable)

Every document the project produces, kept exactly as received. Drop a file into `raw/inbox/`; the
agent classifies it and moves it into `raw/sources/{meetings,governance,reports,registers,contracts,reference}/`
**before** anything cites it, so citations always point at a permanent location. Files here are never
edited or deleted. This is the audit floor: whatever the brain later says, the original is intact and
citable. A messy risk register you feed it stays messy in `raw/` — the *improved* version lives one
layer up.

### Layer 2 — `registers/` (structured truth)

The single source of truth for anything with an ID, an owner and a lifecycle: risks, issues,
assumptions, dependencies, constraints, decisions, actions, stakeholders, requirements. **One file
per item**, with YAML frontmatter for the structured fields and a markdown body for the narrative.

### Layer 3 — `wiki/` (narrative truth)

What the project *means* and how it connects. Meeting syntheses, governance write-ups, workstream
pages, the charter/scope/governance-model/team foundation pages, people, and filed answers. Wiki
pages hold synthesis and link out to register IDs (`RSK-014`, `DEC-003`) rather than restating the
structured data. An `index.md` catalogs the pages; a `log.md` records every operation; a
`coaching-log.md` tracks which lessons the PM has absorbed.

### Layer 4 — `views/` + `STATE.md` (generated)

Derived dashboards, regenerated from the registers and carrying a "do not edit" header: `raid.md`,
`actions.md`, `decisions.md`, `stakeholder-map.md`, and the living `STATE.md`. Because they are
generated, they cannot drift from the registers — the register is always the truth, the view is
always the current picture of it.

## Why registers are a separate layer from the wiki

This is the one deliberate departure from pure Karpathy, and it is load-bearing.

A risk is not narrative. It has a probability, an impact, an owner, a review date and a status that
moves through a defined lifecycle. Bury that inside a prose wiki page and you lose the ability to sort
it, sweep it for staleness, roll it into a RAID table, or track how its severity moved over time. So
structured lifecycle data gets its own layer, sitting between the immutable `raw/` and the narrative
`wiki/`. The wiki still does what it is good at — meaning and connection — and points at the register
for the facts.

## Why one file per item

Every register item is its own file (`registers/risks/RSK-014 Vendor SLA gap.md`) rather than a row
in one big table. Three reasons:

1. **Clean git diffs = a free audit trail.** Change one risk's severity and the commit touches one
   file with a legible before/after. Over a project's life you get a complete, greppable history of
   how every risk, decision and action evolved — the thing status reports systematically hide.
2. **Obsidian renders the frontmatter as properties.** Open the folder in Obsidian and each item is a
   proper record with typed fields, while the registers remain plain markdown that any editor or
   script can read.
3. **Room for narrative.** A good risk is more than five numbers. The body holds the
   cause → risk → effect statement, the mitigations (linked to actions), and the history. A decision's
   body holds the options considered and the rationale. That is what separates a real register from
   lazy furniture, and a row in a spreadsheet has nowhere to put it.

## How views and STATE are generated

The registers are the truth; the views are a projection of it. When an ingest or a change touches the
registers, the agent regenerates the affected views by reading the register files and rendering them
into tables — RAID, actions, decisions, the stakeholder influence/interest map — and refreshes
`STATE.md`. Views are never hand-edited; if a number looks wrong, you fix the register item and
regenerate. (`STATE.md` may optionally carry a small hand-curated "focus this week" header above the
generated block.) This is why the dashboard can always be trusted: it is not a separate artefact that
someone forgot to update, it is a live render of the source of truth.

## What makes it a teaching tool, not just a store

Two mechanisms turn a passive knowledge base into a coach.

### The standards library — the curriculum

`standards/` is a set of plain-markdown good-practice files — risk-quality, rag-evidence,
decision-hygiene, action-quality, stakeholder-coverage, governance-pack, meeting-minutes. Each has the
same shape: the **principle** (why it matters), the **checklist** (what gets tested), **reframe
patterns** (weak → strong, with a worked example), and **when to escalate versus just fix**. This is
the encoded assurance judgment — the actual gift of the project. It is legible and tunable: fork it
and make it yours.

### The coaching pipeline — a stage, not a personality

"Guide and teach" is structural, not a tone the agent adopts. Every path that brings an artefact in —
document ingest, or capturing something you mention in chat — passes through a mandatory coach step:

1. **File as received.** The original goes into `raw/` untouched (or the item is logged from chat).
2. **Score against the standard.** The relevant `standards/` file is applied.
3. **Write the improved version to the register.** Correction made, not just suggested.
4. **Hand back a short before/after + why**, pointing at the standard.

It improves and teaches; it never silently stores a weak artefact, and it never blocks you. A
`coaching-log.md` tracks acceptance: once you have taken a lesson on board about three times, the
agent stops explaining it and just applies the fix — anti-nag by design. A volume control at the top
of the instance `CLAUDE.md` (`coaching: full | light | off`) is set once during the interview.

The [SOUL principles](../template/SOUL.md) map one-to-one onto these mechanisms:
evidence-behind-RAG → `rag-evidence` + the status-drift skill; cause → risk → effect → `risk-quality`;
assumptions logged with a validation date → the assumption schema's `validate_by` machinery;
decision-led governance → the governance-prep skill; and the accountability line — it assures,
advises and drafts, but the human PM owns the decision — enforced as approval gates throughout.

## Kit versus instance

The **kit** is this repo: the bootstrap, the templates, the standards library and the skills. The
**instance** is what the bootstrap generates in the user's folder — their filled-in identity files,
their registers, their wiki, a local (tunable) copy of the standards, and the skills under
`.claude/skills/`. The bootstrap is idempotent: re-running it updates the standards and skills and
scaffolds anything missing, but never touches `raw/`, the registers, or the user's filled-in identity
files.
