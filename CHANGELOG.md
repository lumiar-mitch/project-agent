# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

Nothing yet. See [ROADMAP.md](ROADMAP.md) for where this is going.

## [0.1.1] - 2026-07-22

A patch release fixing eight gaps found in a smoke test. No new features; the instance model,
schemas, standards and skills are all now internally consistent.

### Fixed

- **Clones no longer lose the empty folders.** The bootstrap now writes a `.gitkeep` into every
  otherwise-empty scaffold directory (drop zones, register folders, `views/`, empty wiki sections)
  and tracks them in the initial commit, so a `git clone` of an instance preserves its structure.
- **`title` on every register item.** The `constraint`, `assumption`, `dependency` and `action`
  schemas now list a `title` field (the short label that drives the filename) in their field tables,
  matching their worked examples; fuller fields (`statement`, `description`) stay as body/detail.
  All nine schemas are now consistent on how an item's filename label is defined.
- **Assumption invalidation covers the both-apply case.** An invalidated assumption now spawns an
  `ISS` for any impact already realised **and** an `RSK` for any residual forward exposure — both
  when both apply — with the two linked back to the assumption and to each other, instead of an
  ambiguous "risk or issue".
- **Ingest date fallback for undated documents.** If a document carries no discernible date, ingest
  now files it under the ingest date and marks citations explicitly (e.g.
  `(undated document; ingested 2026-07-22)`); a real document date is still preferred.
- **Ingest wiki-mapping now covers all seven categories.** The `register` category has a defined
  destination (extracted items go to `registers/`, the source to `raw/sources/registers/`, no
  dedicated narrative page, genuine synthesis to `wiki/answers/`).

### Changed

- **Proposed / provisional convention for under-substantiated items.** Items created from an
  interview one-liner, a chat mention, or a lazy register row are now filed as `status: proposed`
  with a new `provisional: true` flag, `owner: TBC`, and clearly-marked agent-suggested ratings —
  a well-formed placeholder awaiting PM confirmation, never invented owners or ratings. Defined
  canonically in the risk schema (§2a) and cross-referenced from the issue/assumption/dependency/
  constraint schemas, `standards/risk-quality.md`, and the instance `CLAUDE.md`.
- **Interview seeding aligned.** The bootstrap and the `project-interview` skill now say the same
  thing: the interview seeds known risks (`RSK`) and current problems (`ISS`) alongside assumptions,
  dependencies and constraints, all using the proposed/provisional convention.
- **`severity` is now a bare integer.** The risk schema stores `severity` as an integer
  (`probability × impact`); the low/medium/high/critical band is presentational and shown only in
  `views/`, not stored in the scalar.
- **Generated-views column spec.** The instance `CLAUDE.md` now defines the exact columns and sort
  order for `raid.md`, `actions.md`, `decisions.md` and `stakeholder-map.md`, so generated tables
  are consistent run-to-run and each carries the "do not edit — generated" header.

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

[Unreleased]: https://github.com/lumiar-mitch/project-agent/compare/v0.1.1...HEAD
[0.1.1]: https://github.com/lumiar-mitch/project-agent/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/lumiar-mitch/project-agent/releases/tag/v0.1.0
