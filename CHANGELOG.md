# Changelog

## 0.2.0 — 2026-06-06

### Install & distribution

- Document `npx skills add XharvaK/maestro` as the primary install path (installs to `~/.agents/skills/maestro`).
- Update manual install docs for `~/.agents/skills/maestro` on Cursor and compatible agents.
- Keep project-scoped install at `.cursor/skills/maestro/` for teams that commit skills per repo.

### Docs

- Remove the 500-line `SKILL.md` cap from contributor guidance; `phases.md` remains the home for deep methodology.
- Add `CHANGELOG.md` for release notes.

### Housekeeping

- Exclude `skills-lock.json` from the repository (user-local lockfile, not part of Maestro).

## 0.1.0 — initial release

- Self-contained 14-phase release-audit orchestrator (`SKILL.md` + `phases.md` + `examples.md`).
- Full, quick, and incident audit tracks with stable finding IDs and Phase 9 synthesis template.
