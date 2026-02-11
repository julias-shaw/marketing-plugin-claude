# Phase 3 Coordinator: Psychographic Profile

**Purpose:** Build a deep psychographic map across four dimensions — Identity, Problems,
Dreams/Desires, and Obstacles — by clustering quotes into themes and filling gaps with
targeted research. This coordinator reads Phase 2 output, organizes it into psychographic
themes, identifies gaps, dispatches per-site subagents to fill them, and writes the final
consolidated profile.

**You are a coordinator subagent.** You may spawn per-site subagents via the Task tool for
gap-filling research.

## Inputs

Before starting, read:
- The research inputs from `00-inputs.md` in the output directory
- The Phase 2 output from `02-voice-of-customer.md` in the output directory
- The per-site agent instructions at the path provided in your Task prompt

Extract from the inputs:
- **Persona** — who the ideal customer is
- **Product** — what's being sold
- **Problems** — what problems the product solves

## Step 1: Cluster Phase 2 Quotes into Themes

Read all quotes from `02-voice-of-customer.md`. Organize them across four psychographic
dimensions. For each dimension, identify at least 5 distinct themes.

**IDENTITY** — How do they see themselves? What labels, roles, or identities do they claim?
**PROBLEMS** — What specific struggles do they face? What keeps them up at night?
**DREAMS / DESIRES** — What do they want their life or situation to look like?
**OBSTACLES** — What stands between them and their goals? What's held them back?

A quote can appear in both Phase 2 (emotional category) and Phase 3 (psychographic theme)
if it serves both purposes. Reuse relevant Phase 2 quotes freely — do not discard them.

For each theme:
- Give it a descriptive name (e.g. "The Overwhelmed Achiever", "Fear of Wasted Money")
- Assign 2-4 quotes that illustrate the theme
- Write a "Pattern" note: what the cluster of quotes reveals about how this group thinks
  (not just what they say, but what it means)

## Step 2: Gap Analysis

After clustering, assess coverage:

- Each dimension should have at least 5 themes with 2-4 quotes each
- Minimum 20 quotes per dimension (80 total)
- Identify dimensions or themes with fewer than 4 quotes — these are gaps

If all dimensions are well-covered (20+ quotes each, 5+ themes each), skip to Step 4.

## Step 3: Gap-Filling Dispatch

If gaps exist:

1. Identify 3-5 sites likely to have conversations relevant to the gap themes. These may
   overlap with Phase 2 sites or be new sites. Tailor the search to the specific gaps.

2. For each site, spawn a per-site subagent via the Task tool. **Launch all gap-filling
   agents in a single message** so they run in parallel.

   Construct each Task prompt like this:

   ```
   Task tool call:
     subagent_type: "general-purpose"
     description: "Phase 3 gap-fill from {site_name}"
     prompt: |
       You are collecting customer quotes from {site_name} to fill gaps in a psychographic profile.

       Read your instructions from {path to prompt-site-agent.md}.

       Site to search: {site_name}
       Search focus: Looking specifically for quotes about {gap description — e.g. "how customers
       identify themselves and what roles they claim" or "obstacles that prevent them from achieving
       their goals"}.
       Persona: {persona}
       Product: {product}
       Problems: {problems}

       Write quotes incrementally to {output_dir}/03-site-{sanitized_site_name}.md.
   ```

3. After all gap-filling agents complete, read the `03-site-*.md` intermediate files and
   merge the new quotes into the existing theme clusters.

## Step 4: Write Final Output

Write `03-psychographic-profile.md` with this structure:

```
---
skill_version: {version from 00-inputs.md frontmatter}
skill_name: market-research
phase: 3-psychographic-profile
---

# Psychographic Profile

## Executive Summary
{2-3 sentences: total quote count, number of themes identified, key psychological patterns}

## Persona Sketch
{5-6 sentence persona sketch capturing the persona's mindset, daily challenges, and driving
motivations — based on the psychographic patterns uncovered, not just demographics}

## Identity

### Theme 1: {theme name}
1. "Quote one." — {author}, [{source}]({url}) ({date})
2. "Quote two." — {author}, [{source}]({url}) ({date})

**Pattern:** {insight about what this cluster reveals about how they think}

### Theme 2: {theme name}
...

## Problems

### Theme 1: {theme name}
...

## Dreams & Desires

### Theme 1: {theme name}
...

## Obstacles

### Theme 1: {theme name}
...
```

Output the frontmatter as raw YAML (no code fences). Read the version from the inputs
file's frontmatter — do not hardcode it.

## Step 5: Clean Up

Delete all intermediate files matching `03-site-*.md` in the output directory.

## Quality Check

After writing the final output, verify:

- At least 5 themes per dimension (20 themes total)
- At least 20 quotes per dimension (80 quotes total)
- Every theme has a Pattern note
- Every quote has source attribution with URL, author, and date

If minimums aren't met, note the shortfall in the Executive Summary.
