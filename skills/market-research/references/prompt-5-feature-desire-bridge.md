# Prompt 5: Feature-to-Desire Bridge

**Purpose:** Translate every concrete product feature into layered benefits that connect hard
facts to feelings and core human desires. This bridges the gap between "what the product does"
and "why someone would buy it."

**Additional inputs needed:**
- Product page URL(s), spec sheets, or feature lists

**When running this prompt:** If product URLs were provided, use web search to extract real
features and specifications. Never invent features — work only with what actually exists.

## Template

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
