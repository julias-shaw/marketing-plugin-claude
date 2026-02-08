# Market Research Prompt Templates

These are the five core prompts for the market research workflow. Each prompt expects three
context inputs that should be collected from the user in Phase 0:

- `{PERSONA}` — description of the ideal customer
- `{PRODUCT}` — what the product/service is
- `{PROBLEMS}` — the core problems it solves

Additional inputs are noted per prompt where applicable.

## Table of Contents

1. [Prompt 1: Market Snapshot](#prompt-1-market-snapshot)
2. [Prompt 2: Voice of Customer](#prompt-2-voice-of-customer)
3. [Prompt 3: Psychographic Profile](#prompt-3-psychographic-profile)
4. [Prompt 4: Awareness & Motivation Map](#prompt-4-awareness--motivation-map)
5. [Prompt 5: Feature-to-Desire Bridge](#prompt-5-feature-to-desire-bridge)

---

## Prompt 1: Market Snapshot

**Purpose:** Establish a clear strategic foundation — who we're targeting, what we're selling,
what problems we solve. This output feeds into every subsequent step.

**Additional inputs needed:**
- Brand website URL (if available)
- 1–2 competitor URLs (if available)

**When running this prompt:** If URLs were provided, use web search to pull real data from
them. Ground the snapshot in actual facts — don't fabricate positioning.

### Template

```
You are a strategic marketing analyst trained in rapid onboarding and positioning discovery.
You specialize in distilling complex business inputs into clear summaries that guide deeper
research.

GOAL: Generate a short, high-clarity writeup that answers three questions: Who are we
targeting, what are we selling, and what problems are we solving?

CONTEXT:
- Ideal customer persona: {PERSONA}
- Product being sold: {PRODUCT}
- Problems the product solves: {PROBLEMS}
- Brand website: {WEBSITE_URL}
- Competitor sites: {COMPETITOR_URLS}

TASK:
Analyze the brand's website and competitor sites (if provided). Write a few short paragraphs
that clearly and confidently answer the three context questions. Keep language simple and
human. Avoid marketing fluff.

Include:
- A one-paragraph sketch of the customer persona (demographics, psychographics, motivations)
- A 1–2 sentence description of the product and how it's positioned
- A short explanation of the core problems this product helps the customer resolve

OUTPUT FORMAT:
Return a written summary in plain paragraphs, not a list or table. Write as if handing it off
to a strategist who needs to understand the market at a glance before diving deeper.
```

---

## Prompt 2: Voice of Customer

**Purpose:** Collect 100 authentic verbatim quotes from real online conversations, organized
by five emotional categories. These quotes become the raw material for writing copy that
sounds like it came from inside the customer's head.

**When running this prompt:** Use web search extensively. Search Reddit, forums, review sites,
Quora, and social media for real conversations. Always cite the actual source. If you cannot
verify a quote, flag it clearly — the user needs to know what's real vs. what might be
AI-generated.

### Template

```
You are a world-class market research analyst specializing in extracting exact customer
language from online communities. You excel at uncovering deep, actionable insights and
capturing authentic, emotionally charged quotes that reflect real emotions, struggles, and
desires.

GOAL: Gather 100 verbatim, word-for-word quotes from real online sources that target
customers use when discussing their fears, frustrations, wants, beliefs, and joys. Also
produce a detailed persona sketch informed by these authentic voices.

CONTEXT:
- Ideal customer persona: {PERSONA}
- Product being sold: {PRODUCT}
- Problems the product solves: {PROBLEMS}

TASK:
1. Identify relevant online communities (subreddits, forums, review sites, social platforms)
   where this persona discusses their problems and desires.

2. Search for real threads and comments from the past 6 months. Ensure insights reflect
   current language and sentiment.

3. Extract raw, word-for-word quotes. For each category below, collect ~20 authentic quotes
   (total: ~100), preserving all slang, typos, and emotion:
   - FEARS: What my prospect is afraid of...
   - FRUSTRATIONS: What my prospect feels frustrated by...
   - WANTS: What my prospect desires...
   - BELIEFS: What my prospect believes to be true...
   - JOYS: What my prospect enjoys or celebrates...

4. Cite every quote with its source (subreddit, forum thread, review page, etc.) for
   traceability. Be sure to include obsidian compatible markdown links to all sources.

5. Synthesize a 5–6 sentence persona sketch that paints a vivid picture of the typical
   customer — their emotional landscape, daily challenges, and driving motivations — based
   entirely on the language and patterns uncovered in your research.

OUTPUT FORMAT:
Return results as a numbered list organized by category. Each quote in quotation marks with
the source labeled. End with the persona sketch in plain language.

CONFIDENCE NOTES:
After the output, add a brief note indicating:
- Which quotes were pulled from verified, linkable sources
- Which quotes are paraphrased or synthesized from multiple sources
- Any areas where source material was thin
```

---

## Prompt 3: Psychographic Profile

**Purpose:** Build a deep psychographic map that goes beyond individual quotes to reveal
thematic patterns in how customers think, identify, struggle, dream, and face obstacles.
Minimum 80 quotes organized by theme with pattern notes.

**When running this prompt:** Use web search to find real conversations. Focus on clustering
quotes by theme — the goal is patterns, not a random list.

### Template

```
You are a senior qualitative researcher using Eugene Schwartz's classic research methods.
Your job is to map the psychographic landscape of a target market using real, verbatim quotes
from online communities.

GOAL: Produce an in-depth psychographic profile across four dimensions — Identity, Problems,
Dreams/Desires, and Obstacles — so that copy can sound like it was written from inside the
community.

CONTEXT:
- Ideal customer persona: {PERSONA}
- Product being sold: {PRODUCT}
- Problems the product solves: {PROBLEMS}

TASK:
1. Locate active conversations in relevant online communities. Focus on posts and comments
   from the last six months.

2. For each of the four categories below, identify at least five distinct THEMES. Under
   every theme, collect 2–4 word-for-word quotes (preserving slang, typos, emotion):

   IDENTITY — How do they see themselves? What labels, roles, or identities do they claim?
   PROBLEMS — What specific struggles do they face? What keeps them up at night?
   DREAMS / DESIRES — What do they want their life or situation to look like?
   OBSTACLES — What stands between them and their goals? What's held them back?

3. Label every quote with its source (subreddit, forum, review site) for traceability.

4. After each theme, write a short "Pattern" note that summarizes the insight across its
   quotes — not just what they're saying, but what it reveals about how they think.

5. When all quotes are collected, write a 5–6 sentence persona sketch capturing the
   persona's mindset, daily challenges, and driving motivations, using only insights from
   your research.

6. Quality check: Confirm at least 20 quotes per category (minimum 80 total).

OUTPUT FORMAT:
Return a clean document structured as:

IDENTITY
  Theme 1: [theme name]
    "Quote one." — [source]
    "Quote two." — [source]
    Pattern: [insight]
  Theme 2: [theme name]
    ...

PROBLEMS
  Theme 1: ...
  (continue through all four categories)

PERSONA SKETCH
  Five to six plain-language sentences bringing the audience to life.
```

---

## Prompt 4: Awareness & Motivation Map

**Purpose:** Map customer questions across Schwartz's five awareness stages, build desire
ladders that drill three levels deep, and expose what customers will say publicly vs. what
they hide vs. what they can't articulate. This is the strategic bridge between understanding
your customer and writing copy that moves them to action.

### Template

```
You are a strategic copywriting researcher applying Eugene Schwartz's awareness framework
to surface deep market desires and stage-specific questions. Your findings will drive copy
that feels insider-authentic.

GOAL: Produce three strategic analysis tables that map the customer journey from unaware to
ready-to-buy, reveal layered motivations, and expose hidden drivers.

CONTEXT:
- Ideal customer persona: {PERSONA}
- Product being sold: {PRODUCT}
- Problems the product solves: {PROBLEMS}

TASK:

1. MARKET AWARENESS LEVELS (Schwartz lens)
   Build a table with five columns representing awareness stages:
   - Unaware: Doesn't know they have a problem
   - Problem Aware: Knows the problem, not the solutions
   - Solution Aware: Knows solutions exist, not your product
   - Product Aware: Knows your product, not convinced yet
   - Most Aware: Ready to buy, just needs the right offer

   For each stage, list the key questions a prospect would naturally ask, using their
   authentic language.

2. MARKET DESIRES EXPANSION
   Identify 5–10 explicit desires this audience expresses.
   For each desire, build a "So I can..." ladder — ask "why?" three times to reveal
   deeper motives.

   Table format:
   | Desire | So I can... (Level 1) | So I can... (Level 2) | So I can... (Level 3) |

3. WILL / WON'T / CAN'T TELL TABLE
   For every desire identified above, capture three layers of candor:
   - Will Tell: What they'll happily say out loud to anyone
   - Won't Tell: What feels too private, embarrassing, or vulnerable to admit
   - Can't Tell: Hidden or subconscious drivers they may not even recognize in themselves

   Table format:
   | Desire | Will Tell | Won't Tell | Can't Tell |

OUTPUT FORMAT:
Return all three tables in order, clearly labeled. Use language that feels real and human —
pull from actual community discussions where possible. Tables should be clean enough to
copy directly into a doc or spreadsheet.
```

---

## Prompt 5: Feature-to-Desire Bridge

**Purpose:** Translate every concrete product feature into layered benefits that connect hard
facts to feelings and core human desires. This bridges the gap between "what the product does"
and "why someone would buy it."

**Additional inputs needed:**
- Product page URL(s), spec sheets, or feature lists

**When running this prompt:** If product URLs were provided, use web search to extract real
features and specifications. Never invent features — work only with what actually exists.

### Template

```
You are a product analyst and copywriting strategist. Your job is to dimensionalize every
meaningful feature of a product, translating hard facts into layered benefits that resonate
on practical, emotional, and desire levels using Eugene Schwartz's research lens.

GOAL: Extract every product feature and build a Feature-to-Desire ladder for each, connecting
concrete specs to human emotions and core desires.

CONTEXT:
- Brand / product: {PRODUCT}
- Primary customer persona: {PERSONA}
- Core problem the product solves: {PROBLEMS}
- Product page link(s): {PRODUCT_URLS}

TASK:

1. LIST RAW FEATURES
   Visit the product page(s) and capture every concrete feature in a bullet list. Include
   materials, measurements, capabilities, components, specifications. Do not add benefit
   language yet — just facts.

2. BUILD THE FEATURE-TO-DESIRE LADDER
   For each feature:
   a. WHY IT EXISTS — Explain in plain language why this feature was included
   b. PERFORMANCE BENEFIT — "So you can..." (what it lets the customer do)
   c. DEEPER BENEFIT — "So you can..." again (the payoff behind the payoff)
   d. DOMINANT EMOTION — What the customer feels when that deeper payoff is achieved
   e. MATCHING DESIRE — Map the emotion to a core human desire (security, freedom, status,
      belonging, mastery, etc.)

3. QUALITY CONTROL
   Ensure all features come from real product facts. Never invent specifications.

OUTPUT FORMAT:
Return a single table with these columns:

| Product | Feature | Why Included | Performance Benefit ("so you can...") | Deeper Benefit ("so you can...") | Dominant Emotion | Matching Desire |

One row per feature. Complete every column before moving to the next feature.
```
