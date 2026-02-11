# Changelog

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
