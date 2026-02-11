# Prompt 2: Voice of Customer

**Purpose:** Collect ~160 authentic verbatim quotes from real online conversations, organized
by eight categories. These quotes become the raw material for writing copy that
sounds like it came from inside the customer's head.

**When running this prompt:** Use web search extensively. Search Reddit, forums, review sites,
Quora, and social media for real conversations. Always cite the actual source. If you cannot
verify a quote, flag it clearly — the user needs to know what's real vs. what might be
AI-generated.

## Template

GOAL: Gather ~160 verbatim, word-for-word quotes from real online sources that target
customers use when discussing their fears, frustrations, wants, beliefs, joys, objections,
buying triggers, and competitor comparisons. Allow the user to override how many quotes to
gather. Also produce a detailed persona sketch informed by these authentic voices. Finally,
export all quotes to a structured CSV file.

CONTEXT:
- Ideal customer persona: {PERSONA}
- Product being sold: {PRODUCT}
- Problems the product solves: {PROBLEMS}

TASK:
1. Identify relevant online communities (subreddits, forums, review sites, social platforms)
   where this persona discusses their problems and desires.

2. Search for real threads and comments from the past 6 months. Ensure insights reflect
   current language and sentiment.

3. Extract raw, word-for-word quotes. For each category below, collect authentic quotes
   (default: ~ 20 per category for a total of ~160 but allow the user to override how
   many to gather), preserving all slang, typos, and emotion:
   - FEARS: What my prospect is afraid of...
   - FRUSTRATIONS: What my prospect feels frustrated by...
   - WANTS: What my prospect desires...
   - BELIEFS: What my prospect believes to be true...
   - JOYS: What my prospect enjoys or celebrates...
   - OBJECTIONS: Reasons they give for not buying or not acting ("I would, but...")
   - TRIGGERS: Events or moments that pushed them to start looking for a solution ("I finally snapped when...")
   - COMPARISONS: How they talk about alternatives or competitors ("I tried X but...")

4. Cite every quote with its source (subreddit, forum thread, review page, etc.) for
   traceability. Be sure to include obsidian compatible markdown links to all sources.

5. Capture the author. Record the username or handle of the person who posted each quote.
   If the author is anonymous or not visible, write "Anonymous".

6. Date every quote. After the source, include the date it was posted in parentheses,
   formatted like (Jan 3, 2025). If the date is not visible on the page, check the Wayback
   Machine (web.archive.org) to find when the content was first captured. If no date can be
   determined, write (Date Unknown).

7. Verify every quote. Before saving a quote, re-visit the source URL and confirm the quote
   actually appears on the page. If the quote cannot be found on the page, discard it and
   find a real replacement. Do not guess or reconstruct quotes from memory — every quote in
   the final output must exist verbatim at its cited source.

8. Synthesize a 5–6 sentence persona sketch that paints a vivid picture of the typical
   customer — their emotional landscape, daily challenges, and driving motivations — based
   entirely on the language and patterns uncovered in your research.

OUTPUT FORMAT:
Return results as a numbered list organized by category. Each quote in quotation marks with
the source labeled and the date in parentheses after the source. Format dates as Mon D, YYYY
(e.g. Jan 3, 2025). Write (Date Unknown) if the date cannot be determined.

Example:
1. "I've tried everything and nothing sticks." — u/habithacker, [r/productivity](https://reddit.com/...) (Mar 12, 2025)
2. "The pricing feels predatory honestly." — Anonymous, [TrustPilot review](https://trustpilot.com/...) (Date Unknown)

End with the persona sketch in plain language.

CSV OUTPUT:
After the dossier content, write all quotes to a file named `voice-of-customer.csv` with
these columns:

| Column   | Description                                                        |
|----------|--------------------------------------------------------------------|
| Quote    | The exact verbatim quote text (no surrounding quotation marks)     |
| Date     | Post date as Mon D, YYYY (e.g. Jan 3, 2025) or "Date Unknown"     |
| Type     | Source type: Reddit, Forum, Review, YouTube, Quora, Social, Other  |
| URL      | Direct URL to the source page                                      |
| Source   | Specific source name (e.g. r/productivity, Amazon, TrustPilot)    |
| Author   | Username or handle of the poster, or "Anonymous" if not available  |
| Category | One of: Fear, Frustration, Want, Belief, Joy, Objection, Trigger, Comparison |

Rules for the CSV:
- Use double quotes around every field value to handle commas and special characters in quotes
- Escape any double quotes inside field values by doubling them ("" inside the field)
- One row per quote, no blank rows
- Include the header row

META FILE:
After creating `voice-of-customer.csv`, also create a companion file named
`voice-of-customer.csv.meta` with the following YAML content:

```yaml
skill_name: market-research
skill_version: {version from SKILL.md metadata.version}
created_at: {today's date as YYYY-MM-DD}
columns: Quote,Date,Type,URL,Source,Author,Category
```

This `.meta` file allows migration tooling to detect the skill version that produced the CSV,
since CSV files cannot contain YAML frontmatter. Always read the version dynamically from
`SKILL.md` `metadata.version` — do not hardcode it.

CONFIDENCE NOTES:
After the output, add a brief note indicating:
- Which quotes were pulled from verified, linkable sources
- Which quotes are paraphrased or synthesized from multiple sources
- Any areas where source material was thin
