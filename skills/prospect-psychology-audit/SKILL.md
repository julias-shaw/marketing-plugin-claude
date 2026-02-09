---
name: prospect-psychology-audit
description: >
  Assess marketing content or customer profiles against three buyer psychology frameworks:
  Eisenberg's Four Buying Temperaments, Hughes' 6MX Decision Pillars, and Schwartz's
  Prospect Awareness Levels. Use this skill whenever the user wants to audit marketing
  content (website copy, landing page, video transcript, ad, email, sales page), evaluate
  how well content appeals to different buyer types, assess an ideal customer profile (ICP)
  or voice-of-customer (VoC) quotes, find blind spots in messaging, or understand which
  psychological profiles their content is serving vs. ignoring. Also trigger when the user
  mentions buyer temperaments, decision styles, awareness levels, persuasion architecture,
  or prospect psychology in the context of marketing content. Works with any text-based
  marketing input — paste it in, upload a file, or provide a URL for analysis.
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

Before conducting any assessment, read the reference files for all three frameworks:
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

Keep the output scannable — the ratings tables are the core deliverable, and the prose sections should be concise. Save the completed audit as a markdown file and present it to the user.

---

## Scoring Principles

These principles help ensure consistent, well-calibrated ratings:

**Ground every rating in observable evidence.** Never rate based on what the content *could* include. Rate based on what's actually there. If there's no evidence for a dimension, the default is Neutral (not Attracts).

**Distinguish "not addressed" from "actively repels."** Content that simply ignores Methodical buyers (no specs, no FAQ, but also no hype) is Neutral. Content that is *all* hype, urgency, and emotional pressure with zero substance actively repels Methodical buyers — that's Repels or Strongly Repels.

**Respect the tension between pillars.** If content strongly activates Conformity ("most popular choice, trusted by thousands"), it will likely score lower on Deviance — and that's expected, not a flaw. Note the tradeoff rather than penalizing it.

**For customer profiles, match language to frameworks.** When a VoC quote says "I just need something that works, I don't have time to research," that's strong Necessity + Spontaneous signal. When they say "I spent weeks comparing every option before choosing," that's Methodical + Investment. Let the customer's own words drive the ratings.

**The awareness level rating is about fit, not quality.** A brilliant Most Aware sales page (discount code, buy button, zero education) would score Neutral for Unaware — and that's correct. The content isn't bad; it's just not built for that stage.

---

## Edge Cases

**Mixed content (e.g., full website with multiple pages):** Assess the overall impression. If distinct pages serve different functions (homepage vs. pricing vs. about), note which pages serve which profiles. The primary rating should reflect the aggregate experience.

**Very short content (e.g., a single ad or headline):** Short content naturally covers fewer dimensions. Rate what's present and mark unaddressed dimensions as Neutral. Don't over-infer from limited material — note the constraint in the synthesis.

**VoC quotes that contradict each other:** If the VoC set comes from multiple customers, different quotes may map to different profiles. Note this explicitly — it likely means the customer base is psychologically diverse, which is useful information for the user.

**Content in a non-English language:** Apply the same frameworks. Buyer psychology is cross-cultural, though cultural context may shift which pillars are baseline expectations vs. differentiators. Note any relevant cultural considerations.
