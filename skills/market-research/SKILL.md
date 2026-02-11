---
name: market-research
metadata:
  version: 1.2.0
  repository: https://github.com/julias-shaw/marketing-plugin-claude
description: >
  Run a structured 5-step AI-powered market research workflow based on Eugene Schwartz's
  research methodology. Produces a comprehensive research dossier that maps customer language,
  psychographics, awareness levels, hidden motivations, and feature-to-desire connections.
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

A 5-step market research workflow that produces a complete customer intelligence dossier.
Based on Eugene Schwartz's classic research methodology — the gold standard for
understanding markets since 1966.

## Output

Two deliverables:

1. A **Markdown research dossier** (see `references/dossier-template.md` for structure) covering:
   market snapshot, voice of customer (~160 quotes), psychographic profile, awareness & motivation
   map, and feature-to-desire bridge.
2. A **`voice-of-customer.csv`** file containing every quote from Phase 2 in a structured,
   filterable format. Columns: `Quote,Date,Type,URL,Source,Author,Category`.

## Workflow

### Version Check

Before starting, read `references/version-check.md` and follow the version check
procedure. Do not skip this step — but if the check fails, warn the user and continue.

### Artifact Migration

If the user provides an existing artifact (a previously generated dossier or CSV file), or
explicitly asks to "migrate this" or "update this to the latest format":

1. Read `references/migration-check.md` and follow the detection procedure.
2. If the artifact is outdated, offer to migrate it before proceeding with any new work.
3. If the user just wants the migration (not a full rerun), perform the migration and stop.

This also applies if the user pastes dossier content inline — check for the `skill_version`
frontmatter to determine whether it's current.

### Phase 0: Gather Inputs

Before running any research, collect three pieces of context from the user. These are required
for every step and should be captured once, then reused throughout.

Ask the user:

1. **Who is your ideal customer?** (demographics, psychographics, or even just a rough description)
2. **What is your product/service?** (what it is, how it's positioned, pricing tier if relevant)
3. **What problems does it solve?** (the core pains or desires it addresses)

Also ask for:
- Brand website URL (if available)
- 1-2 competitor URLs (if available)
- Any existing customer research, testimonials, or review links

Store these inputs — they get pasted into every subsequent step.

If the user has partial answers, that's fine. Step 1 will help fill the gaps.

### Phase 1: Market Snapshot

**Goal:** Establish a clear, concise foundation — target customer, product positioning, core problems.

Read `references/prompt-1-market-snapshot.md` and run it with the user's inputs.

**Output:** A 3–4 paragraph briefing document. Save this — it feeds into every remaining step.

**Tip:** If the user provided a website URL, use web search to pull real information from it.
Don't fabricate positioning — ground it in what actually exists.

### Phase 2: Voice of Customer

**Goal:** Collect authentic customer quotes (~160 by default but allow the user to override this) from real online sources, organized by emotional category.

Read `references/prompt-2-voice-of-customer.md` and run it.

This step uses web search to find real conversations on Reddit, forums, review sites, and
social platforms. The prompt covers all eight categories, quote verification, date attribution,
author capture, and CSV export — follow it as written.

**Output:** Organized quote bank + persona sketch + CSV file.

### Phase 3: Psychographic Profile

**Goal:** Build a deep psychographic map across four dimensions: Identity, Problems, Dreams/Desires, Obstacles.

Read `references/prompt-3-psychographic-profile.md` and run it.

Unlike Phase 2 (which collects individual quotes), this phase looks for **thematic patterns** —
clusters of quotes that reveal how customers think, not just what they say.

**Output:** Themed quote clusters with pattern notes + updated persona sketch.

### Phase 4: Awareness & Motivation Map

**Goal:** Map customer questions across Schwartz's 5 awareness stages, build desire ladders, and expose hidden motivations.

Read `references/prompt-4-awareness-map.md` and run it.

This produces three strategic tables:
1. **Awareness Levels** — Questions buyers ask at each stage (Unaware → Most Aware)
2. **Desire Ladders** — Surface desire → "So I can..." × 3 levels deep
3. **Will / Won't / Can't Tell** — What customers say openly vs. hide vs. can't articulate

**Output:** Three tables ready for use in messaging strategy.

### Phase 5: Feature-to-Desire Bridge

**Goal:** Translate every product feature into layered benefits that connect to emotions and core human desires.

Read `references/prompt-5-feature-desire-bridge.md` and run it.

If the user provided product URLs, use web search to extract real features. Never invent specs.

**Output:** A comprehensive table: Feature → Why It Exists → Performance Benefit → Deeper Benefit → Dominant Emotion → Matching Desire

### Assembly

After all five phases, compile everything into a single research dossier. Use the template in
`references/dossier-template.md` to structure the final output.

**Important:** The output must include YAML frontmatter with `skill_version` set to the value
from `metadata.version` in this file's frontmatter. Read the version dynamically — do not
hardcode it. The dossier template shows the exact format.

Save the dossier as a Markdown file and present it to the user.

## Execution notes

- **Run steps in order.** Each step builds on the last. Don't skip ahead.
- **Use web search aggressively** in Phases 2 and 3 to find real customer language. Reddit,
  Amazon reviews, YouTube comments, Quora, and niche forums are gold mines.
- **Keep the user's original language.** When collecting quotes, preserve slang, typos,
  emotional intensity. Sanitized quotes are useless for copy.
- **The dossier is the deliverable.** The final Markdown file should be something the user can
  print, reference, and share with their team. Make it clean and well-organized.
