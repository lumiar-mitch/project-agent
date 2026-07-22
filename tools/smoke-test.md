# Smoke test

A scripted end-to-end validation a maintainer runs after changing the bootstrap, a template, a
standard or a skill. It checks that a fresh install builds a correct instance, that ingestion coaches
and files correctly, and that a re-run is idempotent. Work top to bottom; each step has an expected
result. If any step fails, stop and fix before release.

**Time:** ~15 minutes. **You need:** Claude Code signed in, and outbound access to the pinned raw URL.

---

## 0. Set up a clean workspace

1. Create a fresh, empty folder outside the repo and outside any Obsidian vault, e.g.
   `~/Code/scratch/brain-test-1/`.
   **Expected:** the folder exists and is empty (`ls -A` returns nothing).

## 1. Run the bootstrap

2. Open the empty folder in Claude Code and paste the one-line command:
   ```
   Read https://raw.githubusercontent.com/lumiar-mitch/project-agent/v0.1.0/bootstrap/BOOTSTRAP.md and build my Project Agent in this folder.
   ```
   **Expected:** Claude fetches the bootstrap and begins an interview rather than dumping files.

3. Answer the interview with a small test project (e.g. "office relocation", role "PM", a sponsor and
   a fortnightly steering committee, coaching `full`).
   **Expected:** the interview covers project, role, governance, document location, and coaching
   level, then reports what it is about to build before writing.

## 2. Verify the interview wrote the identity files and seeded registers

4. Confirm the identity files exist and are filled in with your answers (not template placeholders):
   `PROJECT.md`, `USER.md`, `CLAUDE.md`, `SOUL.md`, `STATE.md`.
   **Expected:** `PROJECT.md` names your test project and its governance; `USER.md` names your role;
   `CLAUDE.md` carries the `coaching: full` config block; `STATE.md` exists with a generated header.

5. Confirm the registers are seeded (any items the interview elicited exist as one-file-per-item under
   the right subfolder, with valid frontmatter).
   **Expected:** e.g. a seeded risk at `registers/risks/RSK-001 ....md` with `owner`, `review`,
   `probability`, `impact` populated and a cause → risk → effect body.

## 3. Verify all template / standard / skill files scaffolded to the correct paths

6. Check the instance skeleton exists:
   **Expected paths present:**
   - `raw/inbox/` (empty) and `raw/sources/{meetings,governance,reports,registers,contracts,reference}/`
   - `registers/_schemas/` plus subfolders: `risks/ issues/ assumptions/ dependencies/ constraints/ decisions/ actions/ stakeholders/ requirements/`
   - `views/` with `raid.md`, `actions.md`, `decisions.md`, `stakeholder-map.md` (each carrying a
     "do not edit — generated" header)
   - `wiki/index.md`, `wiki/log.md`, `wiki/coaching-log.md`, and the foundation pages
   - `standards/` with all seven: `risk-quality`, `rag-evidence`, `decision-hygiene`,
     `action-quality`, `stakeholder-coverage`, `governance-pack`, `meeting-minutes`
   - `.claude/skills/` with all six: `project-interview`, `ingest`, `weekly-review`,
     `risk-register-review`, `status-drift`, `governance-prep`

7. Spot-check that no file contains an unresolved template placeholder (e.g. `{{PROJECT_NAME}}`).
   **Expected:** none in the identity files or seeded registers.

## 4. Ingest a messy risk register

8. Drop the sample messy risk register (see below) into `raw/inbox/` and ask:
   ```
   Ingest my inbox and report what you did.
   ```
   Sample content to save as `raw/inbox/messy-risks.md`:
   ```
   Risk 1: The project might fail. Owner: the team. High risk.
   Risk 2: Budget. Red.
   Risk 3: Vendor didn't deliver the API last week so integration is now blocked.
   ```

9. **Expected — filing:** the file is moved to `raw/sources/registers/` (immutable, unchanged) before
   anything is cited. `raw/inbox/` is empty again.

10. **Expected — extraction + reframe with coach's notes:**
    - "The project might fail" is reframed to a proper cause → risk → effect statement, the owner
      "the team" is rejected (a named owner is required), and a review date is added — with a short
      coach's note pointing at `standards/risk-quality`.
    - "Budget / Red" is challenged as not-yet-a-risk (no event, no owner) and the PM is asked for the
      missing fields.
    - "Vendor didn't deliver … now blocked" is reframed as an **issue**, not a risk (it has already
      happened), and the PM is told why.
    - Each accepted item exists as a one-file register entry with valid frontmatter.

11. **Expected — regeneration:** `views/raid.md` and `STATE.md` are regenerated and reflect the new
    items. Views still carry the "do not edit" header. `wiki/log.md` has a new ingest entry; the
    coaching log records the lessons.

## 5. Verify idempotent re-run

12. Note the current state: record the contents/hashes of a filled identity file (`PROJECT.md`), a
    seeded register item, and the ingested `raw/sources/registers/messy-risks.md`.

13. Re-run the exact bootstrap command from step 2.
    **Expected:** it detects an existing instance and scaffolds only what is missing / refreshes
    standards and skills. It does **not** re-run the interview destructively.

14. Re-check the files from step 12.
    **Expected — nothing clobbered:**
    - `raw/` is byte-for-byte unchanged (sources and their content intact).
    - The register items are unchanged (no reset to seed state, no lost coaching).
    - The filled-in identity files (`PROJECT.md`, `USER.md`, `STATE.md` curated header) are unchanged.
    - Only `standards/` and `.claude/skills/` may have been updated to the current version.

---

## Pass criteria

All steps meet their expected result: a fresh folder produces a correct, fully-scaffolded instance;
ingestion files immutably, extracts, reframes and coaches to standard, and regenerates the views and
STATE; and a re-run is safe (idempotent, never destructive to `raw/`, registers, or filled-in identity
files). Any deviation is a release blocker.
