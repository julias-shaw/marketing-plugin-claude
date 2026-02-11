# Artifact Migration Check

Follow this procedure when the user provides an existing artifact (content audit, customer
profile) to determine whether it needs migrating to the current skill version.

**Current status:** No migrations exist yet. Version 1.2.0 is the first release of this skill
with version stamping. This file defines the detection and chaining procedure so future
versions can add migration files without changing the workflow.

---

## Step 1: Detect the Artifact Version

Read the artifact and check for YAML frontmatter at the top of the file:

```
---
skill_version: X.Y.Z
skill_name: prospect-psychology-audit
---
```

- If frontmatter exists and contains `skill_version`, that is the artifact's version.
- If there is **no frontmatter** or no `skill_version` field, the artifact predates version
  stamping. Since v1.2.0 is the first stamped version, treat it as a v1.0.0 artifact.

---

## Step 2: Read the Current Skill Version

Read the `SKILL.md` file's YAML frontmatter and extract `metadata.version`. This is the
current installed skill version.

---

## Step 3: Compare Versions

Compare the artifact version (Step 1) against the current skill version (Step 2):

- **Artifact version equals current version** → No migration needed. Proceed normally.
- **Artifact version is older than current version** → Check for migration files (Step 4).
- **Artifact version is newer than current version** → Warn the user: "This artifact was
  created with v{artifact} but your installed skill is v{current}. You may want to update
  the skill first." Continue without migrating.

---

## Step 4: Build the Migration Chain

Migrations are applied sequentially. Each migration file in the `migrations/` directory handles
one version step, named as `{from}-to-{to}.md` (e.g. `1.2.0-to-1.3.0.md`).

To migrate from the artifact's version to the current version:

1. Determine the sequence of migration files needed.
2. Check that **every file in the chain exists** in the `migrations/` directory.
3. If any file in the chain is **missing** (which will be the case until future versions add
   migration files), tell the user: "No migration path available for this artifact. Please
   rerun the full skill to regenerate it with the current version."
4. If the full chain exists, read and execute each migration file in order, passing the output
   of each step as input to the next.

---

## Step 5: Confirm Completion

After all migration steps complete, tell the user what was updated and what limitations exist
(each migration file's post-migration message covers this). Save the migrated artifact.
