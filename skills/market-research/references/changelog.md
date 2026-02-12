# Changelog

## 1.6.0

- All source URLs now include Text Fragment directives (`#:~:text=...`) that scroll to and
  highlight the quoted passage when clicked in a browser
- New `text-fragments.md` reference doc provides URL construction rules for per-site subagents
- Per-site agents (`prompt-site-agent.md`) generate text fragment URLs during quote collection
- Phase 2 and 3 coordinators preserve text fragment URLs through consolidation
- CSV `URL` column includes text fragment URLs when available
- Summary dossier Top Quotes section preserves text fragment URLs

## 1.5.0

- Version bump (no structural changes to artifacts)

## 1.4.0

- Restructured skill to use subagent architecture for context efficiency
- Each phase now produces its own standalone markdown file in a `market-research-{slug}/` directory
- Phase 2 and 3 use parallel per-site subagents for deeper, broader web research
- Quotes are written incrementally (partial results preserved if an agent hits limits)
- Lightweight summary dossier (`research-summary.md`) replaces monolithic single-file dossier
- Full quote details live in dedicated phase files (`02-voice-of-customer.md`, `03-psychographic-profile.md`)
- New shared `prompt-site-agent.md` provides consistent instructions for per-site quote collection
- Phase 2 and 3 coordinators automatically clean up intermediate per-site files after consolidation

## 1.3.0

- VOC visualization

## 1.2.0

- Exports all Voice of Customer quotes to `voice-of-customer.csv` with companion `.meta` file
- Added three new quote categories: Objections, Triggers, and Comparisons (~160 quotes total)
- Quotes now include post date (Mon D, YYYY format) with Wayback Machine fallback
- Quotes now include author/username attribution
- Added mandatory quote verification — every quote is re-checked at its source URL before saving
- Quote count is now user-overridable (default: ~20 per category)
- Artifacts now include YAML frontmatter with `skill_version` for migration tracking
- Added artifact migration system — old dossiers can be structurally upgraded without regenerating
- Includes v1.1.0 → v1.2.0 migration (frontmatter, CSV extraction, new sections, `.meta` file)

## 1.1.0

- Initial release — 5-phase Schwartz research workflow
