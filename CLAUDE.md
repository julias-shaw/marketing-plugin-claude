# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A marketing skill plugin for Claude bundling two skills:

- **market-research** — 5-phase Schwartz research workflow using subagent architecture to produce a multi-file customer intelligence package + CSV
- **prospect-psychology-audit** — Eisenberg/Hughes/Schwartz framework assessment of marketing content or buyer profiles

All files are Markdown instructions that Claude reads at runtime. There is no compiled code.

## CI Checks

Run locally before pushing (mirrors `.github/workflows/check-shared-files.yml`):

```bash
# 1. version-check.md files must be identical across skills
diff skills/market-research/references/version-check.md skills/prospect-psychology-audit/references/version-check.md

# 2. Output templates must contain skill_version
grep -l "skill_version" skills/market-research/references/dossier-template.md \
  skills/prospect-psychology-audit/references/content-audit.md \
  skills/prospect-psychology-audit/references/customer-profile.md

# 3. SKILL.md versions must match plugin.json
python3 -c "import json; print(json.load(open('.claude-plugin/plugin.json'))['version'])"
# Compare against metadata.version in each skills/*/SKILL.md frontmatter
```

## Version Synchronization

All versions must match. When bumping:

1. `.claude-plugin/plugin.json` → `version` field
2. Every `skills/*/SKILL.md` → `metadata.version` in YAML frontmatter
3. Every `skills/*/references/changelog.md` → add entry for new version

CI enforces the sync between plugin.json and SKILL.md files on every PR.

## Shared Files

`version-check.md` must be **byte-identical** across all skills. Edit one, copy to all others. CI fails on any diff.

`migration-check.md` is **intentionally different** per skill — each has its own migration history and artifact types.

`prompt-site-agent.md` is shared across Phase 2 and Phase 3 within the market-research skill. It provides consistent instructions for per-site quote collection subagents.

## Skill Structure

```
skills/{skill-name}/
├── SKILL.md              # Skill definition (frontmatter + workflow instructions)
├── references/           # Runtime support files Claude reads during execution
│   ├── version-check.md  # Shared: update check procedure (must be identical)
│   ├── migration-check.md # Per-skill: artifact version detection + migration chaining
│   ├── changelog.md      # Per-skill: version history
│   └── ...               # Skill-specific prompts, templates, frameworks
└── migrations/           # Version upgrade instructions
    └── {from}-to-{to}.md # e.g., 1.1.0-to-1.2.0.md
```

## Market Research Subagent Architecture

The market-research skill uses a subagent architecture where SKILL.md acts as a thin
orchestrator dispatching each phase to dedicated subagents via the Task tool:

- **Phase 0** runs in the main context (input collection only)
- **Phases 1, 4, 5** each dispatch a single subagent
- **Phases 2, 3** dispatch a coordinator subagent that spawns per-site subagents in parallel
- **Summary** dispatches a single subagent to produce `research-summary.md`

The orchestrator never reads prompt reference files directly — only subagents do. This keeps
the main context window small. The `dossier-template.md` file now contains the lightweight
summary template (not the old monolithic dossier template).

## Artifact Versioning

Every artifact a skill produces gets stamped with the skill version so old artifacts can be detected and migrated later without regenerating from scratch.

**Markdown artifacts** (dossiers, audits, phase files) use YAML frontmatter at the top of the file:
```yaml
---
skill_version: 1.2.0
skill_name: market-research
---
```

**CSV artifacts** cannot contain frontmatter, so they get a companion `.meta` file (e.g. `voice-of-customer.csv.meta`):
```yaml
skill_name: market-research
skill_version: 1.2.0
created_at: 2025-05-15
columns: Quote,Date,Type,URL,Source,Author,Category
```

**Rules:**
- `skill_version` is always read dynamically from `SKILL.md` `metadata.version` at runtime — never hardcoded in templates
- Output templates show the frontmatter inside code fences as an example, but include an explicit note to output it as raw YAML (no code fences in the actual artifact)
- Artifacts with no frontmatter predate version stamping and are treated as the oldest known version (v1.0.0 or v1.1.0 depending on the skill)
- CI enforces that all output templates contain `skill_version`

## Artifact Migration System

Migrations upgrade old artifacts structurally to match the current version's format without re-running the full skill. This saves time and tokens when only the format has changed.

**How it works at runtime:**
1. When a user provides an existing artifact, the skill reads `references/migration-check.md`
2. migration-check detects the artifact's version from its frontmatter (or `.meta` file for CSVs)
3. If the artifact is older than the installed skill, the user is offered a migration
4. Migration files are chained sequentially from the artifact's version to the current version

**Migration file naming:** `migrations/{from}-to-{to}.md` (e.g. `1.1.0-to-1.2.0.md`)

**Each migration file contains:**
- Numbered steps for structural changes (add frontmatter, add/rename sections, extract data to new formats, create companion files)
- Specific instructions for what to populate vs. leave as placeholders
- A post-migration message summarizing what was updated and what couldn't be backfilled (requires a full rerun)

**Migration chaining:** To go from v1.0.0 to v1.3.0, the system applies `1.0.0-to-1.1.0.md` → `1.1.0-to-1.2.0.md` → `1.2.0-to-1.3.0.md` in sequence. If any file in the chain is missing, the user is told to rerun the skill from scratch.

**When to create a migration:** Any time a version bump changes the output artifact's structure (new sections, renamed fields, new companion files, changed frontmatter). If the change is content-only (better prompts producing better quotes), no migration is needed.

## Adding a New Skill

1. Create `skills/{name}/SKILL.md` with `name`, `metadata.version`, `metadata.repository`, `description` in frontmatter
2. Copy `version-check.md` from an existing skill (must be identical)
3. Create `migration-check.md` using the stub template (see prospect-psychology-audit for first-release example)
4. Create `migrations/` directory with `.gitkeep`
5. Add `changelog.md`
6. Ensure output templates include `skill_version` frontmatter
7. Match `metadata.version` to `.claude-plugin/plugin.json`
