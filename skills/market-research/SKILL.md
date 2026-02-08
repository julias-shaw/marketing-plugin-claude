---
name: market-research
description: >
  Run a structured 5-step AI-powered market research workflow based on Eugene Schwartz's
  research methodology. Produces a comprehensive research dossier that maps customer language,
  psychographics, awareness levels, hidden motivations, and feature-to-desire connections.
  Use this skill whenever the user wants to deeply understand their target market, do customer
  research, build buyer personas, prepare for copywriting, plan messaging strategy, or says
  things like "research my audience", "understand my customers", "who is my buyer",
  "customer insights", "market analysis for copy", or "voice of customer research".
  Also trigger when the user wants to improve landing pages, emails, or ads by better
  understanding who they're writing to.
---

# Market Research Skill

A 5-step market research workflow that produces a complete customer intelligence dossier.
Based on Eugene Schwartz's classic research methodology — the gold standard for
understanding markets since 1966.

## Output

A single Markdown research dossier (see `references/dossier-template.md` for structure) covering:
market snapshot, voice of customer (100 quotes), psychographic profile, awareness & motivation
map, and feature-to-desire bridge.

## Workflow

### Phase 0: Gather Inputs

Before running any research, collect three pieces of context from the user. These are required
for every step and should be captured once, then reused throughout.

Ask the user:

1. **Who is your ideal customer?** (demographics, psychographics, or even just a rough description)
2. **What is your product/service?** (what it is, how it's positioned, pricing tier if relevant)
3. **What problems does it solve?** (the core pains or desires it addresses)

Also ask for:
- Brand website URL (if available)
- 1–2 competitor URLs (if available)
- Any existing customer research, testimonials, or review links

Store these inputs — they get pasted into every subsequent step.

If the user has partial answers, that's fine. Step 1 will help fill the gaps.

### Phase 1: Market Snapshot

**Goal:** Establish a clear, concise foundation — target customer, product positioning, core problems.

Read `references/prompts.md` → Section "Prompt 1: Market Snapshot" and run it with the user's inputs.

**Output:** A 3–4 paragraph briefing document. Save this — it feeds into every remaining step.

**Tip:** If the user provided a website URL, use web search to pull real information from it.
Don't fabricate positioning — ground it in what actually exists.

### Phase 2: Voice of Customer

**Goal:** Collect 100 authentic customer quotes from real online sources, organized by emotional category.

Read `references/prompts.md` → Section "Prompt 2: Voice of Customer" and run it.

This step uses web search to find real conversations on Reddit, forums, review sites, and
social platforms. For each of the five categories (fears, frustrations, wants, beliefs, joys),
gather ~20 quotes.

**Critical:** Always cite sources. Flag clearly if any quotes could not be verified. AI
hallucination of quotes is a known risk — be transparent about confidence levels.

**Output:** Organized quote bank + persona sketch.

### Phase 3: Psychographic Profile

**Goal:** Build a deep psychographic map across four dimensions: Identity, Problems, Dreams/Desires, Obstacles.

Read `references/prompts.md` → Section "Prompt 3: Psychographic Profile" and run it.

Unlike Phase 2 (which collects individual quotes), this phase looks for **thematic patterns** —
clusters of quotes that reveal how customers think, not just what they say.

**Output:** Themed quote clusters with pattern notes + updated persona sketch.

### Phase 4: Awareness & Motivation Map

**Goal:** Map customer questions across Schwartz's 5 awareness stages, build desire ladders, and expose hidden motivations.

Read `references/prompts.md` → Section "Prompt 4: Awareness & Motivation Map" and run it.

This produces three strategic tables:
1. **Awareness Levels** — Questions buyers ask at each stage (Unaware → Most Aware)
2. **Desire Ladders** — Surface desire → "So I can..." × 3 levels deep
3. **Will / Won't / Can't Tell** — What customers say openly vs. hide vs. can't articulate

**Output:** Three tables ready for use in messaging strategy.

### Phase 5: Feature-to-Desire Bridge

**Goal:** Translate every product feature into layered benefits that connect to emotions and core human desires.

Read `references/prompts.md` → Section "Prompt 5: Feature-to-Desire Bridge" and run it.

If the user provided product URLs, use web search to extract real features. Never invent specs.

**Output:** A comprehensive table: Feature → Why It Exists → Performance Benefit → Deeper Benefit → Dominant Emotion → Matching Desire

### Assembly

After all five phases, compile everything into a single research dossier. Use the template in
`references/dossier-template.md` to structure the final output.

Save the dossier as a Markdown file and present it to the user.

## Execution notes

- **Run steps in order.** Each step builds on the last. Don't skip ahead.
- **Use web search aggressively** in Phases 2 and 3 to find real customer language. Reddit,
  Amazon reviews, YouTube comments, Quora, and niche forums are gold mines.
- **Be honest about confidence.** If you can't verify a quote, say so. If a source is thin,
  flag it. The user needs to trust this research.
- **Keep the user's original language.** When collecting quotes, preserve slang, typos,
  emotional intensity. Sanitized quotes are useless for copy.
- **The dossier is the deliverable.** The final Markdown file should be something the user can
  print, reference, and share with their team. Make it clean and well-organized.
