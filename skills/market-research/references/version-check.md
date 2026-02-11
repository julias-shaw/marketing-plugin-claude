# Version Check Procedure

Follow this procedure before running any skill in the Marketing plugin. It ensures the user
is on the latest version and knows what they're missing if they're not.

This check should be fast and non-blocking. If anything fails, warn the user and continue.

---

## Step 1: Read the Local Version

Read the YAML frontmatter at the top of the skill's own `SKILL.md` file and extract the
`version` and `repository` fields from inside the `metadata` block.

- `metadata.version` is the local version (semver, e.g. `1.2.0`)
- `metadata.repository` is the GitHub repo URL (e.g. `https://github.com/julias-shaw/marketing-plugin-claude`)

These fields are embedded in every skill so the version check works even when the skill is
distributed standalone (e.g. as a zip) without the rest of the plugin.

Extract the owner and repo name from the repository URL to build raw content URLs.

---

## Step 2: Check the Cache

Look for a cache file at `.version-cache` in the skill's own directory (next to `SKILL.md`).
The cache file is a simple two-line text file:

```
<unix_timestamp_of_last_check>
<latest_remote_version>
```

If the cache file exists and the timestamp is **less than 24 hours old**, use the cached
remote version and skip to Step 4.

If the cache file is missing, unreadable, or older than 24 hours, proceed to Step 3.

---

## Step 3: Fetch the Remote Version

Fetch the remote `plugin.json` by reading the GitHub repo's raw content URL:

```
https://raw.githubusercontent.com/{owner}/{repo}/main/.claude-plugin/plugin.json
```

Use whatever web fetching capability is available (WebFetch tool, curl, or any HTTP
request method). No special tools like `gh` CLI are required — this is a plain public URL.

Extract the `version` field from the returned JSON.

**If this fails** (network error, timeout, non-200 response, etc.):
- Tell the user: "Could not check for updates (network unavailable). Continuing with the
  installed version."
- Proceed to run the skill normally. Do not block.

**If it succeeds:**
- Write the current unix timestamp and the remote version to `.version-cache` in the
  skill's own directory (create the file if it doesn't exist)
- Proceed to Step 4

---

## Step 4: Compare Versions

Compare the local version (from Step 1) against the remote version (from cache or Step 3)
using semantic versioning rules:

- Parse both versions as `major.minor.patch`
- If remote is **greater than** local → the user is outdated, go to Step 5
- If remote is **equal to or less than** local → the user is current, proceed to run the
  skill with no message

---

## Step 5: Notify the User

If the user is outdated, show them a concise update notice **before** running the skill.

### 5a: Fetch the Changelog

Determine the skill's directory name (e.g. `market-research` or `prospect-psychology-audit`)
and fetch its changelog from the remote repo:

```
https://raw.githubusercontent.com/{owner}/{repo}/main/skills/{skill-name}/references/changelog.md
```

Extract changelog entries for versions **newer than** the user's local version. Show only
the entries they're missing — not the full changelog.

If the changelog fetch fails, skip it and just report the version numbers.

### 5b: Show the Update Notice

Format the notice like this:

```
Update available: Marketing plugin v{local} → v{remote}

What's new since your version:
{changelog entries for versions between local and remote, inclusive of remote}

To update:
  • Claude Code CLI: run `claude plugin update marketing`
  • Other environments: reinstall the plugin from the marketplace or
    re-clone from {repository_url}

You can skip this update and run the skill now if you prefer.
```

### 5c: Let the User Decide

Ask the user if they want to:
1. **Update now** — if in Claude Code CLI, run `claude plugin update marketing` for them.
   In other environments, show the manual instructions and wait for them to confirm they've
   updated before restarting the skill.
2. **Skip and continue** — proceed to run the skill on the current version.

If the user chooses to skip, run the skill normally. Do not ask again during this
conversation (the 24-hour cache handles suppression across conversations).

