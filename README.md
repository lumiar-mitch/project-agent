# Project Agent

**A local-first project agent and assurance coach you run with Claude Code.**
It reads everything your project produces, keeps proper registers, and stress-tests your
artefacts against good practice — *AI as critic, not author.*

Most AI-for-projects tools try to write your risk register, your status report, your steering
pack. You have probably already watched that produce confident, generic slop. This does the
opposite. It assumes *you* write the artefacts, and its job is to challenge them: chase down the
lazy risk, ask what evidence sits behind a green RAG, find the bad news buried under an "on track",
and prepare the decisions a board actually has to make. It has read every document on your project
and it holds the work to a standard — an agent that also coaches you toward better practice.

Your project's files live in a folder on your machine — no SharePoint, no cloud store, no separate
service, and no accounts beyond Claude Code itself. Project Agent runs *on* Claude, so the documents
and text you ask it to work on are sent to Anthropic's API to be processed, exactly like any Claude
Code session, and handled under Anthropic's data-use terms. Nothing goes anywhere else: no
third-party services, no telemetry, no copy of your project held on someone's server. You keep the
source of truth and you decide what goes in.

---

## What it does

- **Reads your documents.** Drop minutes, board packs, status reports or a contract into
  `raw/inbox/`; it files them immutably, extracts what matters, and updates the brain.
- **Keeps proper registers.** One file per item for risks, issues, assumptions, dependencies,
  constraints, decisions, actions, stakeholders and requirements — structured, owned, dated, and
  version-controlled so you get a clean audit trail for free.
- **Red-teams your risk register.** It enforces *cause → risk → effect*, insists on a named owner
  and a live review date, and reframes a "risk" that has already happened as an issue — and tells
  you why.
- **Hunts watermelons in your status.** Green-outside / red-inside: schedule slip behind a green,
  open risks under an "on track", a RAG colour with no evidence behind it. It surfaces them early.
- **Preps decision-led governance.** It frames steering inputs around the calls the board cannot
  delegate — funding, tolerance breaches, accepting material risk, continue or stop — not status
  for its own sake.
- **Answers with citations.** "What changed this week?" and "what were the actions from last
  month's steering session?" — answered from your own documents, cited by register ID and source,
  never invented.
- **Coaches as it goes.** It improves an artefact on the way in and hands back a short before/after
  with the *why*, pointing at the standard. Once you have accepted a lesson a few times, it stops
  explaining and just applies the fix. A coach, not a nag.

## The four-layer model

Built on the [Karpathy LLM-wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f),
specialised for a single project:

```
raw/        immutable facts — every document, exactly as received; never edited
  → registers/   structured truth — one file per item, with an ID, an owner, a lifecycle
  → wiki/        narrative truth — what it means and how it connects; links to register IDs
  → views/ + STATE.md   derived dashboards — regenerated from the registers, never hand-edited
```

Registers are a layer of their own because a risk or a decision is structured, lifecycle data —
it does not belong buried in prose. The wiki holds meaning; the registers hold truth; the views
are generated. See [`docs/architecture.md`](docs/architecture.md) for the full explainer.

## Quick start

You need Claude Code (it runs in the desktop app — no terminal required) and an empty folder for
your project. Then paste this one line into Claude Code:

```
Read https://raw.githubusercontent.com/lumiar-mitch/project-agent/v0.1.0/bootstrap/BOOTSTRAP.md and build my Project Agent in this folder.
```

Claude fetches the bootstrap, interviews you about the project (what is it, what is your role,
where do the documents live, how much coaching do you want), scaffolds the whole structure filled
in with your answers, and finishes by inviting you to drop a document in `raw/inbox/` and ask
*"what changed this week?"*. No git, no cloning, nothing to configure.

Full walkthrough for non-technical PMs: **[GETTING-STARTED.md](GETTING-STARTED.md)**.

## What it will NOT do

- **It will not decide for you.** Scope, priority, risk ratings, risk acceptance, stakeholder
  commitments and the final call belong to you. It preps the decision and stops at the
  accountability line.
- **It will not fabricate.** If something isn't in your documents, it says so. Every fact is cited.
- **It will not hide bad news.** It will not soften a status to make it look reassuring. Bad news
  early beats good news late.
- **It will not send your project anywhere but Claude.** No SharePoint, no cloud sync, no telemetry,
  no third-party services. Your files stay in your folder; the only thing that leaves is the content
  you ask Claude to process, which goes to Anthropic like any Claude Code session.

## FAQ

**Do I need to know how to code?**
No. You install Claude Code, sign in, open an empty folder and paste one line. The agent builds and
runs everything. If you can drop a file into a folder, you can use this.

**Where does my data go?**
Your files live in a folder on your computer — that folder is the source of truth. There is no
server, database or account holding your project, and this kit adds no telemetry or uploads of its
own. The one important caveat: Project Agent *is* Claude, so whenever you ask it to read or work on
something, that content is sent to Anthropic's API to be processed — exactly as in any Claude Code
session — and is covered by Anthropic's data-use and privacy terms. Nothing is sent anywhere else.
Treat it like any AI tool: follow your organisation's policy on what you put into Claude.

**Does it work behind corporate IT?**
The install fetches one file from GitHub, so you need outbound access to
`raw.githubusercontent.com` — most networks allow this, some locked-down proxies block it (there is
a workaround in [GETTING-STARTED.md](GETTING-STARTED.md)). After install, the only outbound traffic
is Claude Code's normal connection to Anthropic to run the model — there is no other service to
reach. Because nothing connects to SharePoint, Teams or any internal system, there is no infosec
integration to stand up (though your usual policy on what may be sent to Claude still applies).

**What's the catch?**
There isn't one. It is free and MIT-licensed — fork it, tune the standards, share what you build.
It is made by a PM who would rather ship the critique than keep posting it. If it is useful, the
best thanks is to improve a standard and send it back.

## Demo

A worked example instance lives in [`docs/example-project/`](docs/example-project/) — a small,
fictional project showing what a healthy brain looks like.

## Licence

MIT. See [LICENSE](LICENSE). Copyright 2026 Mitchell Knight.
