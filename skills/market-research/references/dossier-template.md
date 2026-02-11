# Summary Dossier Template

Use this template to assemble the `research-summary.md` file after all five phases are
complete. This summary provides an overview of each phase with key highlights — the full
details live in the individual phase files.

**Important:** Always read the current version from the `00-inputs.md` file's frontmatter
`skill_version` field and insert it below. Do not hardcode the version number. Output the
frontmatter below as raw YAML (the `---` delimiters only, no surrounding code fences).

---

```
---
skill_version: {version from 00-inputs.md frontmatter}
skill_name: market-research
---
```

# Market Research Summary: {PRODUCT_NAME}

**Prepared for:** {CLIENT_OR_BRAND}
**Date:** {DATE}
**Methodology:** Eugene Schwartz Research Framework, AI-assisted
**Architecture:** Subagent-based multi-file research package

---

## 1. Market Snapshot

{Brief summary from 01-market-snapshot.md — the executive summary and key positioning points.
Keep to 1-2 paragraphs. Full details in `01-market-snapshot.md`.}

---

## 2. Voice of Customer Overview

**Total quotes:** {count from 02-voice-of-customer.md}
**Sources searched:** {number of distinct sources}

### Category Breakdown

| Category | Count | Key Theme |
|----------|-------|-----------|
| Fears | {n} | {dominant theme} |
| Frustrations | {n} | {dominant theme} |
| Wants | {n} | {dominant theme} |
| Beliefs | {n} | {dominant theme} |
| Joys | {n} | {dominant theme} |
| Objections | {n} | {dominant theme} |
| Triggers | {n} | {dominant theme} |
| Comparisons | {n} | {dominant theme} |

### Persona Sketch

{Copy the persona sketch from 02-voice-of-customer.md}

### Top Quotes

{Pick the 5-8 most powerful quotes across all categories — the ones that best capture the
customer's voice. Include full attribution.}

*Full quote bank with all {count} quotes: see `02-voice-of-customer.md`*
*Filterable CSV: see `voice-of-customer.csv`*

---

## 3. Psychographic Profile Overview

### Key Patterns

{Summarize the top 3-5 psychographic patterns from 03-psychographic-profile.md. For each,
include the theme name and the Pattern insight — but not all the individual quotes.}

### Persona Sketch

{Copy the persona sketch from 03-psychographic-profile.md}

*Full themed clusters with all quotes: see `03-psychographic-profile.md`*

---

## 4. Awareness & Motivation Map

{Copy the three tables in full from 04-awareness-motivation-map.md — these are compact and
are the core strategic output of this phase.}

### Market Awareness Levels

| Stage | Key Questions They're Asking |
|-------|------------------------------|
| Unaware | {questions} |
| Problem Aware | {questions} |
| Solution Aware | {questions} |
| Product Aware | {questions} |
| Most Aware | {questions} |

### Desire Ladders

| Desire | So I can... (L1) | So I can... (L2) | So I can... (L3) |
|--------|-------------------|-------------------|-------------------|
| {desire} | {level 1} | {level 2} | {level 3} |

### Hidden Motivations

| Desire | Will Tell | Won't Tell | Can't Tell |
|--------|-----------|------------|------------|
| {desire} | {public} | {private} | {subconscious} |

---

## 5. Feature-to-Desire Bridge

{Copy the table in full from 05-feature-desire-bridge.md — this is compact and is the core
output of this phase.}

| Product | Feature | Why Included | Performance Benefit | Deeper Benefit | Dominant Emotion | Matching Desire |
|---------|---------|-------------|--------------------|--------------------|------------------|-----------------|
| {name} | {feature} | {why} | {benefit 1} | {benefit 2} | {emotion} | {desire} |

---

## How to Use These Files

- **For headlines & hooks:** Pull from the strongest quotes in `02-voice-of-customer.md`
- **For email sequences:** Use the Awareness Levels table (Section 4 above) to match messaging to buyer stage
- **For landing pages:** Lead with Desires and Emotions from Section 5, backed by Features
- **For objection handling:** Use Objections quotes in `02-voice-of-customer.md` + Won't Tell and Can't Tell columns above
- **For retargeting & win-back:** Use Triggers in `02-voice-of-customer.md` to time messages around catalytic moments
- **For competitive positioning:** Use Comparisons in `02-voice-of-customer.md` to address how prospects evaluate alternatives
- **For brand voice:** Use the Identity themes in `03-psychographic-profile.md` to mirror how customers see themselves
- **For ad copy:** Combine Fears/Frustrations from `02-voice-of-customer.md` with Dreams/Desires from `03-psychographic-profile.md`
- **For spreadsheet analysis:** Import `voice-of-customer.csv` to filter, sort, and pivot quotes by category, source, or date

---

## File Manifest

| File | What It Contains |
|------|-----------------|
| `00-inputs.md` | Research inputs: persona, product, problems, URLs |
| `01-market-snapshot.md` | Strategic foundation: who we're targeting, what we're selling, why |
| `02-voice-of-customer.md` | ~160 categorized customer quotes with full attribution |
| `03-psychographic-profile.md` | Themed psychographic clusters across Identity, Problems, Dreams, Obstacles |
| `04-awareness-motivation-map.md` | Awareness levels, desire ladders, hidden motivations tables |
| `05-feature-desire-bridge.md` | Feature → benefit → emotion → desire mapping table |
| `voice-of-customer.csv` | All VoC quotes in structured CSV for filtering and analysis |
| `voice-of-customer.csv.meta` | CSV metadata (version, columns) for migration tooling |
| `research-summary.md` | This file — overview and navigation guide |

---

*Research methodology based on Eugene Schwartz's Breakthrough Advertising framework.*
*AI-assisted research — all quotes should be verified before use in final copy.*
