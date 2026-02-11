---
name: market-research
metadata:
  version: 1.4.0
  repository: https://github.com/julias-shaw/marketing-plugin-claude
description: >
  Run a structured 5-step AI-powered market research workflow based on Eugene Schwartz's
  research methodology. Produces a multi-file research package: market snapshot, voice of
  customer (~160 quotes), psychographic profile, awareness & motivation map, feature-to-desire
  bridge, and a summary dossier. Uses subagent architecture for deep web research without
  hitting context limits.
  Use this skill whenever the user wants to deeply understand their target market, do customer
  research, build buyer personas, prepare for copywriting, plan messaging strategy, or says
  things like "research my audience", "understand my customers", "who is my buyer",
  "customer insights", "market analysis for copy", "voice of customer research",
  "Schwartz research", "customer language mining", "psychographic research",
  "awareness level mapping", "desire ladder", or "feature-to-benefit analysis".
  Also trigger when the user wants to improve landing pages, emails, or ads by better
  understanding who they're writing to, or when they ask for a "research dossier",
  "customer intelligence report", or "market deep dive".
---

# Market Research Skill

A 5-step market research workflow that produces a complete customer intelligence package.
Based on Eugene Schwartz's classic research methodology — the gold standard for
understanding markets since 1966.

This skill uses a **subagent architecture**: the main context acts as a thin orchestrator,
dispatching each research phase to a dedicated subagent via the Task tool. This prevents
context exhaustion during web-heavy phases and enables parallel research across multiple sites.

## Output

A directory named `market-research-{product-slug}/` containing:

| File | Description |
|------|-------------|
| `00-inputs.md` | Captured research inputs (persona, product, problems, URLs) |
| `01-market-snapshot.md` | Phase 1: Strategic foundation — who, what, why |
| `02-voice-of-customer.md` | Phase 2: ~160 categorized quotes from real online sources |
| `03-psychographic-profile.md` | Phase 3: Themed psychographic clusters across 4 dimensions |
| `04-awareness-motivation-map.md` | Phase 4: Awareness levels, desire ladders, hidden motivations |
| `05-feature-desire-bridge.md` | Phase 5: Feature → benefit → emotion → desire mapping |
| `voice-of-customer.csv` | All Phase 2 quotes in structured CSV format |
| `voice-of-customer.csv.meta` | YAML metadata for the CSV (version, columns) |
| `research-summary.md` | Lightweight summary dossier linking all phase files |

## Workflow

### Version Check

Before starting, read `references/version-check.md` and follow the version check
procedure. Do not skip this step — but if the check fails, warn the user and continue.

### Artifact Migration

If the user provides an existing artifact (a previously generated dossier, phase file, or CSV),
or explicitly asks to "migrate this" or "update this to the latest format":

1. Read `references/migration-check.md` and follow the detection procedure.
2. If the artifact is outdated, offer to migrate it before proceeding with any new work.
3. If the user just wants the migration (not a full rerun), perform the migration and stop.

This also applies if the user pastes dossier content inline — check for the `skill_version`
frontmatter to determine whether it's current.

### Phase 0: Gather Inputs

This phase runs directly in the main context (no subagent needed).

Collect these inputs from the user:

1. **Who is your ideal customer?** (demographics, psychographics, or even just a rough description)
2. **What is your product/service?** (what it is, how it's positioned, pricing tier if relevant)
3. **What problems does it solve?** (the core pains or desires it addresses)

Also ask for:
- Brand website URL (if available)
- 1-2 competitor URLs (if available)
- Any existing customer research, testimonials, or review links

If the user has partial answers, that's fine — Phase 1 will help fill gaps.

**Create output directory:** Derive a slug from the product name (lowercase, hyphens for
spaces, strip special characters). Create directory `market-research-{slug}/` in the current
working directory.

**Write `00-inputs.md`:** Save all collected inputs to `{output_dir}/00-inputs.md` in this format:

```
---
skill_version: {read from metadata.version above}
skill_name: market-research
---

# Research Inputs

## Ideal Customer Persona
{persona description}

## Product / Service
{product description}

## Problems It Solves
{problems description}

## URLs
- Brand website: {url or "Not provided"}
- Competitor sites: {urls or "Not provided"}
- Existing research: {urls or "Not provided"}
```

Note the `skill_version` in the frontmatter example above. Read the version dynamically from
`metadata.version` in this file's frontmatter — do not hardcode it. Output the frontmatter
as raw YAML (the `---` delimiters only, no surrounding code fences).

Store the `{output_dir}` path and the path to this skill's directory (`{skill_dir}` — the
directory containing this SKILL.md file) for use in all subsequent Task prompts.

### Phase 1: Market Snapshot

**Goal:** Establish a clear, concise foundation — target customer, product positioning, core problems.

Dispatch a single subagent:

```
Task tool call:
  subagent_type: "general-purpose"
  description: "Phase 1 market snapshot"
  prompt: |
    You are running Phase 1 of a market research workflow.

    Read the research inputs from {output_dir}/00-inputs.md.
    Read the detailed instructions from {skill_dir}/references/prompt-1-market-snapshot.md.

    Follow the instructions using the inputs. If URLs were provided, use web search to pull
    real information from them. Don't fabricate positioning — ground it in what actually exists.

    Start the output with YAML frontmatter:
    ---
    skill_version: {version}
    skill_name: market-research
    phase: 1-market-snapshot
    ---

    (Read the version from the inputs file's frontmatter. Output frontmatter as raw YAML,
    no code fences.)

    Then write a brief 2-3 sentence executive summary before the full content.

    Write your complete output to {output_dir}/01-market-snapshot.md.
```

Wait for the subagent to complete before proceeding to Phase 2.

### Phase 2: Voice of Customer

**Goal:** Collect ~160 authentic customer quotes from real online sources, organized by
emotional category.

Dispatch a coordinator subagent:

```
Task tool call:
  subagent_type: "general-purpose"
  description: "Phase 2 VoC coordinator"
  prompt: |
    You are the Phase 2 coordinator for a market research workflow.

    Read the research inputs from {output_dir}/00-inputs.md.
    Read your coordinator instructions from {skill_dir}/references/prompt-2-voice-of-customer.md.
    The per-site agent instructions are at {skill_dir}/references/prompt-site-agent.md.
    The output directory is {output_dir}/.

    Follow the coordinator instructions. They will tell you to:
    1. Survey search to identify 8-15 relevant sites
    2. Dispatch per-site subagents in parallel via Task tool
    3. Consolidate results into the final output files
    4. Clean up intermediate per-site files
```

The coordinator subagent will internally spawn per-site subagents via the Task tool. Each
per-site agent gets its own context window for web searching, which is why this architecture
avoids context exhaustion.

Wait for the coordinator to complete before proceeding to Phase 3.

### Phase 3: Psychographic Profile

**Goal:** Build a deep psychographic map across four dimensions: Identity, Problems,
Dreams/Desires, Obstacles.

Dispatch a coordinator subagent:

```
Task tool call:
  subagent_type: "general-purpose"
  description: "Phase 3 psychographic coordinator"
  prompt: |
    You are the Phase 3 coordinator for a market research workflow.

    Read the research inputs from {output_dir}/00-inputs.md.
    Read the Phase 2 output from {output_dir}/02-voice-of-customer.md.
    Read your coordinator instructions from {skill_dir}/references/prompt-3-psychographic-profile.md.
    The per-site agent instructions are at {skill_dir}/references/prompt-site-agent.md.
    The output directory is {output_dir}/.

    Follow the coordinator instructions. They will tell you to:
    1. Cluster Phase 2 quotes into psychographic themes
    2. Identify gaps in coverage
    3. Dispatch per-site subagents for gap-filling if needed
    4. Consolidate into the final psychographic profile
    5. Clean up intermediate per-site files
```

Wait for the coordinator to complete before proceeding to Phase 4.

### Phase 4: Awareness & Motivation Map

**Goal:** Map customer questions across Schwartz's 5 awareness stages, build desire ladders,
and expose hidden motivations.

Dispatch a single subagent:

```
Task tool call:
  subagent_type: "general-purpose"
  description: "Phase 4 awareness map"
  prompt: |
    You are running Phase 4 of a market research workflow.

    Read the research inputs from {output_dir}/00-inputs.md.
    Read the Phase 2 output from {output_dir}/02-voice-of-customer.md.
    Read the Phase 3 output from {output_dir}/03-psychographic-profile.md.
    Read the detailed instructions from {skill_dir}/references/prompt-4-awareness-map.md.

    Follow the instructions. Ground the awareness levels, desire ladders, and hidden
    motivations in the real customer language from Phases 2 and 3. Use the actual quotes
    and patterns you read — don't invent generic examples.

    Start the output with YAML frontmatter:
    ---
    skill_version: {version}
    skill_name: market-research
    phase: 4-awareness-motivation-map
    ---

    (Read the version from the inputs file's frontmatter. Output frontmatter as raw YAML,
    no code fences.)

    Then write a brief 2-3 sentence executive summary before the full content.

    Write your complete output to {output_dir}/04-awareness-motivation-map.md.
```

Wait for the subagent to complete before proceeding to Phase 5.

### Phase 5: Feature-to-Desire Bridge

**Goal:** Translate every product feature into layered benefits connecting facts to feelings
and core human desires.

Dispatch a single subagent:

```
Task tool call:
  subagent_type: "general-purpose"
  description: "Phase 5 feature-desire bridge"
  prompt: |
    You are running Phase 5 of a market research workflow.

    Read the research inputs from {output_dir}/00-inputs.md.
    Read the Phase 2 output from {output_dir}/02-voice-of-customer.md.
    Read the Phase 3 output from {output_dir}/03-psychographic-profile.md.
    Read the Phase 4 output from {output_dir}/04-awareness-motivation-map.md.
    Read the detailed instructions from {skill_dir}/references/prompt-5-feature-desire-bridge.md.

    Follow the instructions. If product URLs were provided in the inputs, use web search to
    extract real features. Never invent features — work only with what actually exists.

    Ground the emotion and desire columns in the real customer language from prior phases.

    Start the output with YAML frontmatter:
    ---
    skill_version: {version}
    skill_name: market-research
    phase: 5-feature-desire-bridge
    ---

    (Read the version from the inputs file's frontmatter. Output frontmatter as raw YAML,
    no code fences.)

    Then write a brief 2-3 sentence executive summary before the full content.

    Write your complete output to {output_dir}/05-feature-desire-bridge.md.
```

Wait for the subagent to complete before proceeding to the summary.

### Summary Assembly

**Goal:** Produce a lightweight summary dossier that links to all phase files.

Dispatch a single subagent:

```
Task tool call:
  subagent_type: "general-purpose"
  description: "Summary dossier assembly"
  prompt: |
    You are assembling the final summary for a market research workflow.

    Read all phase output files:
    - {output_dir}/00-inputs.md
    - {output_dir}/01-market-snapshot.md
    - {output_dir}/02-voice-of-customer.md
    - {output_dir}/03-psychographic-profile.md
    - {output_dir}/04-awareness-motivation-map.md
    - {output_dir}/05-feature-desire-bridge.md

    Read the summary template from {skill_dir}/references/dossier-template.md.

    Follow the template to produce a summary dossier. The summary should contain:
    - Overviews and key findings from each phase (NOT all 160 quotes — just highlights)
    - The full awareness/motivation tables and feature-desire bridge table (these are compact)
    - A file manifest showing what each output file contains
    - Guidance on how to use the research files

    Write the summary to {output_dir}/research-summary.md.
```

### Completion

After the summary subagent finishes, confirm to the user that all files have been written.
List the output directory contents and briefly describe what each file contains.

## Execution Notes

- **Run phases in order.** Each phase builds on the last. The orchestrator (this context)
  dispatches them sequentially.
- **Phases 2 and 3 have internal parallelism.** Their coordinators spawn per-site subagents
  in parallel. The orchestrator doesn't need to manage this — the coordinator handles it.
- **The orchestrator should NOT read reference prompt files.** Only subagents read them. This
  keeps the main context minimal. The only files the orchestrator reads directly are
  `version-check.md` and `migration-check.md`.
- **Intermediate cleanup.** Phase 2 and 3 coordinators delete their `02-site-*.md` and
  `03-site-*.md` intermediate files after consolidation. The user's output directory should
  only contain the final files listed in the Output section above.
- **If a subagent fails or hits limits,** inform the user which phase failed and suggest
  rerunning just that phase. Partial results from per-site agents are preserved in
  intermediate files until consolidation.
