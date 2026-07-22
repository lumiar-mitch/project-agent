# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

Nothing yet. See [ROADMAP.md](ROADMAP.md) for where this is going.

## [0.1.0] — 2026-07-22

The initial scaffold. A local-first, forkable Project Agent you run with Claude Code —
AI as critic, not author.

### Added

- **Four-layer instance model** — `raw/` (immutable sources) → `registers/` (structured,
  one-file-per-item truth) → `wiki/` (narrative) → `views/` + `STATE.md` (generated dashboards).
  Registers are an explicit layer of their own, sitting between immutable facts and narrative.
- **Nine register schemas**, one file per item with YAML frontmatter and a coached body:
  risk, issue, assumption, dependency, constraint, decision, action, stakeholder, requirement.
  Each encodes good practice — named owners, live review dates, cause → risk → effect,
  options-considered, owner-and-due.
- **Seven standards** (the good-practice library the agent coaches against): risk-quality,
  rag-evidence, decision-hygiene, action-quality, stakeholder-coverage, governance-pack,
  meeting-minutes.
- **Six skills**: project-interview, ingest, weekly-review, risk-register-review, status-drift,
  governance-prep.
- **Bootstrap installer** — an executable prompt (`bootstrap/BOOTSTRAP.md`, mirrored to a gist)
  that interviews the PM, fills the identity files, scaffolds the structure, and installs the
  standards and skills. Idempotent on re-run: scaffolds only what is missing, never touches `raw/`,
  the registers, or filled-in identity files.
- **Local-first raw-folder ingestion** — drop any document into `raw/inbox/`; it is filed
  immutably in `raw/sources/`, items are extracted and coached into the registers, contradictions
  are flagged, and the views and `STATE.md` are regenerated. No SharePoint, no cloud, no accounts
  beyond Claude Code.
- **Identity and operating files** — `SOUL.md` (the assurance mindset and the accountability
  line), `CLAUDE.md` (the schema and workflows), `PROJECT.md`, `USER.md`.
- Repo meta and docs: README, GETTING-STARTED, LICENSE (MIT), this changelog, ROADMAP,
  `docs/architecture.md`, a worked `docs/example-project/`, and a maintainer smoke test.

[Unreleased]: https://github.com/lumiar-mitch/project-agent/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/lumiar-mitch/project-agent/releases/tag/v0.1.0
