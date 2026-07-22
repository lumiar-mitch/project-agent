# BOOTSTRAP — Project Agent

You are Claude Code, running inside an empty (or partly-scaffolded) folder that will become a
**Project Agent** instance: a local-first, project-management and assurance/coaching
agent. This file is your bootstrap script. Follow it top to bottom. It is **idempotent** — safe to
re-run (see step 6).

The instructions below are addressed to you, the executing agent.

---

## 0. Before you start

Set the pinned release base URL you'll fetch from:

```
BASE_URL = https://raw.githubusercontent.com/lumiar-mitch/project-agent/v0.1.0/
```

Everything you scaffold comes from this pinned tag — never `main` — so an instance is reproducible
and can be told to "update to v0.2.0" later by re-running with a new tag.

---

## 1. Greet and explain

Greet the PM briefly and tell them what you're about to do, in plain language:

> "I'll set up a Project Agent here. First I'll ask you about the project in four short
> blocks — you can skip any question and I'll chase it later. Then I'll scaffold the folders,
> registers, standards and skills, and you'll be ready to drop documents in or just talk to me."

Keep it short. Don't lecture.

---

## 2. Run the staged project interview

Ask in **four blocks**, one block at a time. Use structured questions where you can. **Never block**
on an answer: if the PM doesn't know, or says "skip", write that fact under **PROJECT.md → Open
particulars** and move on. As each fact is answered, write it into `PROJECT.md` in the right section,
or seed the matching register item.

**Block A — Identity & intent**
- Project name
- One-line objective
- Sponsor
- Why now / the driver
- Success criteria
→ write to `PROJECT.md` (Identity, Success criteria).

**Block B — Scope**
- Top ~5 deliverables
- Explicit exclusions (what this project is deliberately NOT doing)
→ write to `PROJECT.md` (Scope). Optionally seed `REQ-###` / `DEL` items if the PM is specific.

**Block C — Governance & people**
- Governance forums + cadence (stand-up, SteerCo, board…)
- Who decides what (decision rights)
- The team
- Key stakeholders
→ write forums/decision-rights to `PROJECT.md` (Governance); seed a `STK-###` stakeholder item for
each key stakeholder named; capture the team in `wiki/foundation/team.md`.

**Block D — Hard facts**
- Budget
- Key dates / milestones
- Known constraints, risks, assumptions
→ write budget/dates to `PROJECT.md` (Hard facts); seed `CON-###`, `RSK-###`, `ASM-###` items for
each constraint/risk/assumption named, and summarise + link them in `PROJECT.md`.

Also fill `USER.md` from whatever the PM tells you about themselves (name, role, org, reporting line,
how they like you to work). Anything unanswered → `PROJECT.md → Open particulars` as an unchecked box.

---

## 3. Set the posture (ask once)

Ask one combined question for the two config settings, then write them into the `CLAUDE.md` config
block:

- **Coaching:** `full` (recommended — I improve artefacts and teach you why), `light` (fix and note
  briefly), or `off` (fix silently).
- **Autonomy:** `standard` (recommended — I act on local reversible work, then report) or `tight`
  (I ask before writing to registers/wiki/views/STATE).

Update the `coaching:` and `autonomy:` values in the scaffolded `CLAUDE.md` to match.

---

## 4. Fetch and scaffold from the manifest

Fetch `bootstrap/manifest.yaml` from `BASE_URL`. For every entry, fetch the `source` file from
`BASE_URL + source` and write it to its `target` path in this instance, creating parent directories
as needed:

- `mode: verbatim` — write the file exactly as fetched.
- `mode: fill-in` — write it, then fill any `{{placeholders}}` you already have answers for from the
  interview; leave the rest as placeholders for later.

Also create every empty directory the manifest lists under `directories:` (so the drop zones and
register folders exist from the start).

If a fetch fails (e.g. a corporate proxy blocks `raw.githubusercontent.com`), stop and tell the PM
plainly which URL failed and that the repo must be reachable at the pinned tag — don't fabricate file
contents.

---

## 5. Initialise git (silently)

Run `git init` in the instance root and make a single initial commit ("bootstrap: scaffold PM Second
Brain instance"). Do this quietly — mention it in one line at the end, don't make a ceremony of it.
Git history gives the PM human-edit detection, an audit trail, and safe reverts.

---

## 6. Be idempotent

On a re-run:
- Scaffold only what is **missing**. Skip any target that already exists.
- **Never** touch anything under `raw/`, anything in `registers/`, or any identity file the PM has
  already filled in (`PROJECT.md`, `USER.md`, `CLAUDE.md` config, `SOUL.md` if edited).
- It is safe to add newly-listed template/standard/skill files that a previous version didn't have.
- If nothing is missing, say so and stop.

---

## 7. Finish

Close with a short, plain hand-off:

> "You're ready. Drop a document in `raw/inbox/`, or just tell me about the project. Try asking me
> **'what changed this week?'** once there's something to report."

Don't over-explain. The PM can start immediately.
