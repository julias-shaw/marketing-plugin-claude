---
name: prospect-psychology-audit
metadata:
  version: 1.3.0
  repository: https://github.com/julias-shaw/marketing-plugin-claude
description: >
  Assess marketing content or customer profiles against three buyer psychology frameworks:
  Eisenberg's Four Buying Temperaments, Hughes' 6MX Decision Pillars, and Schwartz's
  Prospect Awareness Levels. Use this skill whenever the user wants to audit marketing
  content (website copy, landing page, video transcript, ad, email, sales page), evaluate
  how well content appeals to different buyer types, assess an ideal customer profile (ICP)
  or voice-of-customer (VoC) quotes, find blind spots in messaging, or understand which
  psychological profiles their content is serving vs. ignoring. Also trigger when the user
  mentions buyer temperaments, decision styles, awareness levels, persuasion architecture,
  prospect psychology, "score my copy", "audit my landing page", "buyer personality analysis",
  "messaging blind spots", "who does my content attract", or "psychological profile of my
  audience" in the context of marketing content. Works with any text-based marketing input —
  paste it in, upload a file, or provide a URL for analysis.
---

# Prospect Psychology Audit

Assess marketing content or customer profiles against three behavioral frameworks to reveal who the messaging attracts, who it repels, and where the psychological blind spots are.

## Frameworks

This skill uses three complementary models, each viewing buyer behavior from a different angle:

| Framework | What It Measures | Source |
|-----------|-----------------|--------|
| **Eisenberg Temperaments** | How buyers process information and make decisions (fast/slow × logic/emotion) | Bryan & Jeffrey Eisenberg, John Quarto-vonTivadar — Persuasion Architecture® |
| **Hughes Decision Pillars** | The dominant psychological lens through which buyers filter choices | Chase Hughes — Six-Minute X-Ray (6MX) |
| **Schwartz Awareness Levels** | Where the prospect sits on their journey from ignorance to purchase-readiness | Eugene Schwartz — Breakthrough Advertising |

Before conducting any assessment, read `references/version-check.md` and follow the
version check procedure. Do not skip this step — but if the check fails, warn the user and
continue.

If the user provides an existing artifact (a previously generated content audit or customer
profile), read `references/migration-check.md` and follow the detection procedure. If the
artifact is outdated, offer to migrate it before proceeding.

Then read the reference files for all three frameworks:
- `references/eisenberg-temperaments.md`
- `references/hughes-decision-pillars.md`
- `references/schwartz-awareness-levels.md`

These contain detailed profiles, scoring criteria, and tension patterns that inform every rating.

---

## Two Assessment Modes

### Mode 1: Content Audit

**Input:** Marketing content — website copy, landing page, video transcript, advertisement, email, sales page, or any persuasive text.

**What you're answering:** "Who does this content attract, who does it repel, and what awareness levels does it speak to?"

### Mode 2: Customer Profile Audit

**Input:** An ideal customer profile (ICP), a set of voice-of-customer (VoC) quotes, survey responses, or a customer persona description.

**What you're answering:** "What buyer psychology does this customer exhibit, and which frameworks best describe how they think and decide?"

The output structure is the same for both modes. The difference is the analytical lens:
- In **Content Audit** mode, you're rating how well the *content* appeals to each profile.
- In **Customer Profile Audit** mode, you're rating how strongly the *customer* exhibits each profile's characteristics.

---

## Assessment Process

### Step 1: Identify the Input

Determine what you're working with:
- If it's marketing content → Content Audit mode
- If it's an ICP, persona, or VoC quotes → Customer Profile Audit mode
- If unclear, ask the user

### Step 2: Read the Content Carefully

Before scoring anything, read through the entire input and take note of:
- **Tone and energy:** Is it fast/urgent or slow/methodical? Emotional or analytical?
- **Proof elements:** What evidence is presented? Data, testimonials, certifications, case studies?
- **Social signals:** Who is referenced? Experts, peers, celebrities, communities?
- **Positioning:** Is this positioned as mainstream/safe, innovative/new, or contrarian/different?
- **Problem framing:** Does it surface a problem, articulate a known problem, compare solutions, handle objections, or go straight to the offer?
- **Action orientation:** What is the reader/viewer asked to do? How much friction exists?

### Step 3: Score Each Framework

Work through each framework systematically. For every dimension, provide:
1. **The rating** (from the scale for that framework)
2. **A brief justification** citing specific content elements that support the rating (1-3 sentences)

Read `references/scoring-guide.md` for calibration principles and edge-case guidance before scoring.

#### Eisenberg Temperaments (4 ratings)

Rate each: **Strongly Repels | Repels | Neutral | Attracts | Strongly Attracts**

- Competitive (NT)
- Spontaneous (SP)
- Humanistic (NF)
- Methodical (SJ)

#### Hughes Decision Pillars (6 ratings)

Rate each: **Strongly Repels | Repels | Neutral | Attracts | Strongly Attracts**

- Deviance
- Novelty
- Social
- Conformity
- Investment
- Necessity

#### Schwartz Awareness Levels (5 ratings)

Rate each: **Strongly Mismatched | Mismatched | Neutral | Appeals | Strongly Appeals**

- Unaware
- Problem Aware
- Solution Aware
- Product Aware
- Most Aware

### Step 4: Synthesize

After scoring, provide:

1. **Primary Profile:** The 1-2 temperaments, 1-2 decision pillars, and 1-2 awareness levels this content/customer most strongly aligns with. This is the "bullseye audience" the content is built for.

2. **Blind Spots:** The temperaments and pillars rated Neutral or below that represent missed opportunities. For a content audit, these are buyer types being left out. For a customer audit, these are psychological dimensions the customer doesn't exhibit (useful for knowing what messaging *won't* work on them).

3. **Tension Flags:** Note any inherent contradictions in the content (e.g., trying to be both "the industry standard" and "the contrarian choice") or in the customer profile (e.g., VoC quotes that show both novelty-seeking and conformity-seeking).

4. **Recommendations** (Content Audit) or **Messaging Implications** (Customer Profile Audit):
   - For Content Audits: 2-4 specific, actionable suggestions for broadening the content's psychological appeal without diluting its strengths. Prioritize the biggest gaps with the simplest fixes.
   - For Customer Profile Audits: 2-4 actionable implications for how to communicate with this customer effectively, plus what messaging approaches to avoid based on their weak or repelling dimensions.

---

## Output Format

Each mode has its own template. Read the appropriate template before writing the output — it contains the exact structure, section headings, and guidance for each field.

- **Content Audit** → use `references/content-audit.md`
- **Customer Profile Audit** → use `references/customer-profile.md`

The two templates share the same three rating tables but differ in their Synthesis sections. The key difference: Content Audits end with **Recommendations** (how to improve the content), while Customer Profile Audits end with **Messaging Implications** (how to communicate with this customer based on their profile).

**Important:** The output must include YAML frontmatter with `skill_version` set to the value
from `metadata.version` in this file's frontmatter. Read the version dynamically — do not
hardcode it. The output templates show the exact format.

Keep the output scannable — the ratings tables are the core deliverable, and the prose sections should be concise. Save the completed audit as a markdown file and present it to the user.
