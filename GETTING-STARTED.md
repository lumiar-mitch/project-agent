# Getting started

This is the full walkthrough for a project manager who does not consider themselves technical.
There is no coding. You install one app, sign in, open a folder, and paste one line. Fifteen
minutes, most of it the download.

By the end you will have a working Project Agent: a folder on your machine that has read your
documents, keeps your registers, and will tell you what changed this week.

---

## 1. Install Claude Code

Claude Code is the tool that does the work. It now runs inside the **desktop app** (and the web
app) — you do not need a terminal or a command line.

- Go to the official install guide: **https://docs.claude.com/en/docs/claude-code**
- Follow the steps for your operating system (Windows or macOS).
- Open the app once it is installed.

> You will need a Claude account. A paid plan (Pro or Team) gives you enough usage to run a project
> brain comfortably. This is the only account or subscription involved.

## 2. Sign in

Open Claude Code and sign in with your Claude account. That is the whole setup — there are no other
logins, API keys, or connectors to configure. Nothing here connects to SharePoint, Teams or any
work system.

## 3. Create an empty folder for your project

Make a new, **empty** folder somewhere sensible on your machine — for example
`Documents/acme-website-brain`. One folder per project.

Then point Claude Code at that folder (in the app, use *Open folder* / *Open project* and choose
the one you just made). Everything the brain creates will live inside this folder and nowhere else.

> Keep it empty to start. The agent is careful never to clobber your own files, but a clean folder
> makes the first run obvious.

## 4. Paste the one-line bootstrap command

In Claude Code, with your empty folder open, paste this and send it:

```
Read https://raw.githubusercontent.com/lumiar-mitch/project-agent/v0.1.1/bootstrap/BOOTSTRAP.md and build my Project Agent in this folder.
```

That URL is the **bootstrap** — an executable set of instructions (also published as a gist for
easy sharing). Claude fetches it and starts building. You are not copying a template; you are
watching an agent construct working software from a document. That *is* the pitch.

## 5. Answer the interview

The agent will interview you before it writes anything. Expect questions like:

- What is this project? (name, goal, rough timeline)
- What is your role, and who do you report to?
- What governance does it have? (a steering committee? a sponsor? how often does it meet?)
- Where do your documents currently live, and what will you feed it first?
- How much coaching do you want — **full**, **light** or **off**? (Full is the recommended default:
  it is the point of the tool. You can change it later.)

Answer in plain language. From your answers it fills in the identity files (`PROJECT.md`,
`USER.md`), seeds the registers, and scaffolds the whole structure — registers, standards, skills,
the wiki and the generated views.

When it finishes you will have a folder that looks roughly like this:

```
your-project-brain/
├── PROJECT.md · USER.md · STATE.md · CLAUDE.md · SOUL.md
├── raw/inbox/        ← drop documents here
│   └── sources/      ← where they get filed, immutably
├── registers/        ← risks, decisions, actions, … (one file per item)
├── wiki/             ← the narrative brain
├── views/            ← generated dashboards (raid.md, actions.md, …)
└── standards/        ← the good-practice library it coaches against
```

## 6. Feed it a document and ask what changed

This is the everyday loop. Take any real project document — last week's status report, the minutes
from a meeting, a board pack, a messy risk register — and drop the file into `raw/inbox/`.

Then, in Claude Code, say:

```
Ingest my inbox, then tell me what changed this week.
```

The agent reads the document, files it immutably in `raw/sources/`, pulls out the risks, decisions
and actions, coaches anything weak (and shows you the before/after with a short why), updates the
registers and the wiki, regenerates the dashboards, and then answers your question — with citations
back to the source.

From here, just keep dropping documents in and asking questions:

- *"What are my top three worries right now, with the evidence?"*
- *"What were the actions from last month's steering session, and which are overdue?"*
- *"Red-team my risk register."*
- *"Prep me for Thursday's steering committee."*

You can also ask it to extend itself — *"create me a skill for a daily standup summary"* — and it
will write one.

---

## Troubleshooting

**The install command fails / it can't read the URL.**
Some corporate networks block `raw.githubusercontent.com` at the proxy. To check, try opening the
URL from step 4 in your browser — if it does not load, your network is blocking it. Options:

- Run the install from a personal machine or a network that isn't behind the corporate proxy, then
  copy the folder across.
- Ask Claude Code to fetch the bootstrap from the gist mirror instead (same content, different host)
  — the gist link is on the project's GitHub page.
- Once installed, the proxy only matters for that first fetch of the template files (and for future
  updates). From then on, the only outbound connection is Claude Code's normal link to Anthropic to
  run the model — there is nothing else to reach.

**Where did my files go?**
Everything is inside the folder you opened in step 3 — your files aren't stored on any server or
third-party service. (The content itself is of course sent to Anthropic to be processed when you ask
the agent to work on it, like any Claude session.) Your original documents are copied into
`raw/sources/` and never modified. If you cannot see a file, ask the agent
*"where did you file the document I just added?"* and it will tell you the path.

**I want to update to a newer version.**
Re-run the same one-line command from step 4 (bump the version number in the URL when a new release
lands, e.g. `.../v0.2.0/...`). The bootstrap is **idempotent**: it scaffolds only what is missing
and updates the standards and skills. It will **never** touch your `raw/` documents, your registers,
or your filled-in identity files. Your data and your judgment are safe across updates.

**It got something wrong.**
Tell it. The brain is designed to be corrected — it files what it received as-is in `raw/`, so the
original is always intact, and you can revert or adjust anything in the registers. It is a coach and
a colleague, not the final word. You own the decisions.
