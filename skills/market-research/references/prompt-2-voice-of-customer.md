# Phase 2 Coordinator: Voice of Customer

**Purpose:** Coordinate the collection of ~160 authentic verbatim quotes from real online
conversations, organized by eight emotional categories. This coordinator identifies relevant
sites, dispatches per-site subagents in parallel, and consolidates their results.

**You are a coordinator subagent.** You will spawn per-site subagents via the Task tool to
do the actual web searching. This keeps each agent's context focused on a single site.

## Inputs

Before starting, read:
- The research inputs from `00-inputs.md` in the output directory (passed in your Task prompt)
- The per-site agent instructions at the path provided in your Task prompt

Extract from the inputs:
- **Persona** — who the ideal customer is
- **Product** — what's being sold
- **Problems** — what problems the product solves
- **URLs** — brand website, competitor sites, existing research

## Step 1: Survey Search

Do 3-5 web searches to identify online communities where this persona discusses their
problems and desires. Look for:

- **Reddit** — Specific subreddits (not just r/all). Search for the persona's problems and
  the product category. Aim for 3-5 distinct subreddits.
- **Review sites** — Amazon reviews, G2, Capterra, TrustPilot, or niche review platforms
  relevant to the product category.
- **Forums** — Niche forums, Facebook groups, Discord servers (if publicly indexed), or
  community sites.
- **Q&A sites** — Quora topics, StackExchange sites relevant to the persona.
- **YouTube** — Comment sections on relevant videos, channels.
- **Social media** — Twitter/X threads, LinkedIn posts (if publicly indexed).

**Target: 8-15 distinct sites.** Be specific — not "Reddit" but "r/productivity" and
"r/getdisciplined". Not "Amazon" but "Amazon reviews for [specific product category]".

Write your site list before proceeding to Step 2.

## Step 2: Dispatch Per-Site Agents

For each site identified in Step 1, spawn a per-site subagent via the Task tool. **Launch
all per-site agents in a single message** so they run in parallel.

Construct each Task prompt like this:

```
Task tool call:
  subagent_type: "general-purpose"
  description: "VoC quotes from {site_name}"
  prompt: |
    You are collecting customer quotes from {site_name}.

    Read your instructions from {path to prompt-site-agent.md}.
    Read the text fragment URL reference from {path to text-fragments.md}.

    Site to search: {site_name} ({site_url if applicable})
    Search focus: Look for quotes revealing fears, frustrations, wants, beliefs, joys,
    objections, buying triggers, and competitor comparisons related to:
    Persona: {persona}
    Product: {product}
    Problems: {problems}

    Write quotes incrementally to {output_dir}/02-site-{sanitized_site_name}.md.
    (Sanitize the site name: lowercase, replace spaces and special chars with hyphens.)
```

**Important:** Dispatch ALL per-site agents in a single message with multiple Task calls
so they run in parallel. Do not wait for one to finish before launching the next.

## Step 3: Consolidation

After ALL per-site agents have completed:

1. **Read all intermediate files** matching `02-site-*.md` in the output directory.

2. **Categorize every quote** into one of eight categories:
   - **Fears** — What the prospect is afraid of
   - **Frustrations** — What the prospect feels frustrated by
   - **Wants** — What the prospect desires
   - **Beliefs** — What the prospect believes to be true
   - **Joys** — What the prospect enjoys or celebrates
   - **Objections** — Reasons they give for not buying or acting ("I would, but...")
   - **Triggers** — Events or moments that pushed them to seek a solution ("I finally snapped when...")
   - **Comparisons** — How they talk about alternatives or competitors ("I tried X but...")

   Some quotes may fit multiple categories — assign the most dominant one.

3. **Write `02-voice-of-customer.md`** with this structure:

   ```
   ---
   skill_version: {version from 00-inputs.md frontmatter}
   skill_name: market-research
   phase: 2-voice-of-customer
   ---

   # Voice of Customer

   ## Executive Summary
   {2-3 sentences: total quote count, number of sources searched, key emotional themes found}

   ## Persona Sketch
   {5-6 sentence persona sketch based on the language patterns across all quotes — their
   emotional landscape, daily challenges, and driving motivations}

   ## Fears
   {numbered quotes with attribution}

   ## Frustrations
   {numbered quotes with attribution}

   ## Wants
   {numbered quotes with attribution}

   ## Beliefs
   {numbered quotes with attribution}

   ## Joys
   {numbered quotes with attribution}

   ## Objections
   {numbered quotes with attribution}

   ## Triggers
   {numbered quotes with attribution}

   ## Comparisons
   {numbered quotes with attribution}

   ## Confidence Notes
   - Which categories had strong coverage vs. thin coverage
   - Which sources were richest
   - Any quotes that could not be verified
   ```

   Output the frontmatter as raw YAML (no code fences). Read the version from the inputs
   file's frontmatter — do not hardcode it.

   Each quote should be formatted as:
   ```
   1. "Exact verbatim quote." — {author}, [{source}]({url with text fragment}) ({date})
   ```

   **Preserve text fragment URLs.** Per-site agents append `#:~:text=...` text fragments to
   source URLs so links scroll to the quoted passage. When consolidating quotes from
   intermediate files, keep these text fragment URLs intact — do not strip them.

4. **Write `voice-of-customer.csv`** containing every quote with these columns:

   | Column   | Description |
   |----------|-------------|
   | Quote    | The exact verbatim quote text (no surrounding quotation marks) |
   | Date     | Post date as Mon D, YYYY (convert relative dates; "Date Unknown" only as last resort) |
   | Type     | Source type: Reddit, Forum, Review, YouTube, Quora, Social, Other |
   | URL      | Direct URL to the source page, including `#:~:text=` text fragment when available |
   | Source   | Specific source name (e.g. r/productivity, Amazon, TrustPilot) |
   | Author   | Username or handle, or "Anonymous" |
   | Category | One of: Fear, Frustration, Want, Belief, Joy, Objection, Trigger, Comparison |

   CSV rules:
   - Use double quotes around every field value
   - Escape any double quotes inside field values by doubling them
   - One row per quote, no blank rows
   - Include the header row

5. **Write `voice-of-customer.csv.meta`** companion file:

   ```yaml
   skill_name: market-research
   skill_version: {version from 00-inputs.md frontmatter}
   created_at: {today's date as YYYY-MM-DD}
   columns: Quote,Date,Type,URL,Source,Author,Category
   ```

6. **Delete all intermediate files** matching `02-site-*.md` in the output directory.

## Quality Check

**Target: ~160 quotes total (~20 per category).** After consolidation, check:

- If any category has fewer than 10 quotes, note it prominently in the Confidence Notes.
- If total quote count is below 100, note which sources were thin and what topics lacked
  coverage.
- The quote count is a default — if the orchestrator or user specified a different target,
  use that instead.
