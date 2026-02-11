# Artifact Migration Check

Follow this procedure when the user provides an existing artifact (dossier, CSV, audit report)
to determine whether it needs migrating to the current skill version.

---

## Step 1: Detect the Artifact Version

Read the artifact and check for YAML frontmatter at the top of the file:

```
---
skill_version: X.Y.Z
skill_name: market-research
---
```

- If frontmatter exists and contains `skill_version`, that is the artifact's version.
- If there is **no frontmatter** or no `skill_version` field, treat the artifact as **v1.0.0**
  (the first version).
- For **CSV files**, check for a companion `.meta` file (e.g. `voice-of-customer.csv.meta`)
  instead of frontmatter. Read `skill_version` from the `.meta` YAML. If no `.meta` file
  exists, treat the CSV as v1.1.0.

---

## Step 2: Read the Current Skill Version

Read the `SKILL.md` file's YAML frontmatter and extract `metadata.version`. This is the
current installed skill version.

---

## Step 3: Compare Versions

Compare the artifact version (Step 1) against the current skill version (Step 2):

- **Artifact version equals current version** → No migration needed. Proceed normally.
- **Artifact version is older than current version** → Migration available. Go to Step 4.
- **Artifact version is newer than current version** → The artifact was created by a newer
  skill version than what's installed. Warn the user: "This artifact was created with v{artifact}
  but your installed skill is v{current}. You may want to update the skill first." Continue
  without migrating.

---

## Step 4: Offer Migration

Tell the user:

> This {artifact type} was created with market-research v{artifact version}. The current
> version is v{current version}. I can migrate it to the new format, which will add
> {brief description of what changes}. Want me to migrate it?

Wait for the user to confirm before proceeding.

---

## Step 5: Build the Migration Chain

Migrations are applied sequentially. Each migration file in the `migrations/` directory handles
one version step, named as `{from}-to-{to}.md` (e.g. `1.1.0-to-1.2.0.md`).

To migrate from the artifact's version to the current version:

1. Determine the sequence of migration files needed. For example, migrating from v1.1.0 to
   v1.3.0 would require: `1.1.0-to-1.2.0.md` then `1.2.0-to-1.3.0.md`.
2. Check that **every file in the chain exists** in the `migrations/` directory.
3. If any file in the chain is **missing**, tell the user: "Migration path incomplete — the
   migration file for v{from} to v{to} is missing. Please rerun the full skill to regenerate
   this artifact from scratch instead."
4. If the full chain exists, read and execute each migration file in order, passing the output
   of each step as input to the next.

---

## Step 6: Confirm Completion

After all migration steps complete, tell the user what was updated and what limitations exist
(each migration file's post-migration message covers this). Save the migrated artifact.
