---
name: ingest
description: Use this when a document lands in raw/inbox, or the user points you at a file to process ("ingest this", "here are the minutes", "process my inbox"). Runs the full pipeline — classify, file, extract to registers, coach, contradiction-check, update wiki, regenerate views — and returns one consolidated report. No step is skippable.
---

# Ingest

The one pipeline every incoming document passes through. Order matters and no step is optional.
`raw/` is immutable: you file the artefact exactly as received and write every improvement to the
register, never to the source.

## 1. Read fully

Read the entire document before doing anything else. If it is long, read it end to end anyway —
extraction and coaching depend on the whole picture (an "on track" on page 1 is judged against a
slipped date on page 6).

## 2. Classify

Assign exactly one category:
`meeting` | `governance` | `status-report` | `register` | `charter/reference` | `contract` | `other`.
When ambiguous, pick the dominant purpose and note the ambiguity in the final report.

## 3. File to raw/sources — BEFORE you cite anything

Move the file from `raw/inbox/` to `raw/sources/<category>/YYYY-MM-DD Title.ext`, where the date is
the document's own date (meeting date, report period, signing date), not today's. **Date fallback:**
if the document has no discernible date of its own, use the **ingest date** (today) for the filename,
and mark it explicitly in every citation of that source, e.g.
`(undated document; ingested 2026-07-22)`. A real document date is always preferred — only fall back
when none can be established. Map categories to folders: meeting→`meetings`, governance→`governance`,
status-report→`reports`, register→`registers`, charter/reference→`reference`, contract→`contracts`,
other→`reference`. Do this move first so every citation you write points at the permanent path. Never
edit or delete the source once filed.

## 4. Extract structured items to registers — DEDUPE first

For every risk, issue, assumption, dependency, constraint, decision, action, stakeholder,
requirement, or deliverable in the document:

1. **Check for an existing open item first.** Search the relevant register for a match by subject,
   owner, and substance — not just by title text. 
2. **Update-with-history vs new:** if it matches an open item, append to that item's **History**
   (dated line, source link) and update changed fields — do not create a duplicate. If it is
   genuinely new, create `registers/<type>/<PREFIX>-### Title.md` with the next free ID for that
   prefix (RSK, ISS, ASM, DEP, CON, DEC, ACT, STK, REQ, DEL — IDs are monotonic per prefix).
3. Populate the schema fields for that type (see `registers/_schemas/`). Enforce the structural
   rules as you go:
   - An **action** with no owner or no due date is not yet an action — capture it but flag the gap;
     do not invent either.
   - A **"risk" that has already happened** is reframed as an **issue** (`from_risk`), and you say
     why in the report.
   - An **assumption** marked invalidated must spawn a linked risk or issue.
   - A **decision** needs options considered; a one-option decision gets coached (step 5).
4. Set `origin` to the source path and add source links with absolute dates.

## 5. Coach — MANDATORY, every ingest

For each extracted item (and the artefact as a whole where relevant — a whole risk register, a
whole status report), score it against the relevant standard:

| Item / artefact | Standard |
|---|---|
| Risk | `standards/risk-quality.md` |
| Status report / RAG colour | `standards/rag-evidence.md` |
| Decision | `standards/decision-hygiene.md` |
| Action | `standards/action-quality.md` |
| Stakeholder coverage | `standards/stakeholder-coverage.md` |
| Governance pack | `standards/governance-pack.md` |
| Meeting minutes | `standards/meeting-minutes.md` |

Write the **improved version into the register item** (raw stays as received). Then, per the
coaching posture in the instance CLAUDE.md config (`coaching: full|light|off`, default **full**):

- **full:** for each fix, give a 3-line coach's note — before → after → why — plus a pointer to the
  standard by name (e.g. "see `standards/risk-quality.md` on cause→risk→effect"). After a lesson has
  been accepted ~3 times (tracked in `wiki/coaching-log.md`), **graduate to silent**: apply the fix
  without the note.
- **light:** apply the fix, one-line note, no worked before/after.
- **off:** apply the fix silently; still log the pattern.

You improve, draft and advise. You never set or change a **rating, a decision, a risk acceptance,
or a stakeholder commitment** on the human's behalf — surface the proposed rating and let them own
it. Log accepted/graduating lessons and standing patterns in `wiki/coaching-log.md`.

## 6. Contradiction check — flag, never overwrite

Compare every extracted fact against existing register items, PROJECT.md, and prior sources. Where
the new source disagrees with what the brain already holds (a date moved, a rating changed, a
"resolved" item reappearing), **flag it** in the affected item's body and in the report:

```
> [!warning] Conflict: <old claim> (source, date) vs <new claim> (source, date)
```

Never silently pick a version or resolve it yourself. Leave the flag until a source or the human
settles it.

## 7. Update the wiki

Create or update the narrative pages this source touches:
meeting→`wiki/meetings/`, governance→`wiki/governance/`, status-report→`wiki/answers/` or the
relevant workstream page, **register→no dedicated narrative page** (the extracted items already live
in `registers/` and the source stays in `raw/sources/registers/`; file any genuine *synthesis* of
what the register revealed — a pattern, a coverage gap, a comparison — in `wiki/answers/`),
charter/reference→`wiki/foundation/`, contract→`wiki/foundation/` (or the relevant workstream page),
other→the most relevant existing page, people→`wiki/people/`. Wiki pages are synthesis (what it
means, how it connects) and link to register IDs — never restate the register tables. Update
`sources:` counts and `updated:` dates on touched pages.

## 8. Regenerate derived layers

Regenerate every affected `views/` file (`raid.md`, `actions.md`, `decisions.md`,
`stakeholder-map.md`) from the registers, and refresh `STATE.md`. These are generated artefacts with
a "do not edit" header — rebuild them, never hand-patch.

## 9. Update index and log

- Add any new wiki pages to `wiki/index.md`.
- Append `wiki/log.md`: `## [YYYY-MM-DD] ingest | <Title>` with what was read, the category, items
  extracted (with IDs), coaching notes, and conflicts flagged.

## 10. One consolidated report to the PM

Return a single report (do not narrate step by step in chat as you go). Include:

- **Filed:** the source's new path and category.
- **Extracted:** each item with its ID and a one-line summary; mark new vs updated-with-history.
- **Coaching:** the notes (before/after/why + standard) for full mode, or a one-line summary for
  light/off.
- **Conflicts:** every `[!warning]` you raised.
- **Open questions:** missing owners/dates, ambiguous classification, anything needing the human's
  call. End on these — they are the human's to close, and none of them block the ingest.
