# Per-Site Quote Collection Agent

Instructions for a subagent that collects customer quotes from a single online source.
This file is shared by Phase 2 (Voice of Customer) and Phase 3 (Psychographic Profile)
coordinators. Each per-site agent receives its parameters via the Task prompt.

## Input Parameters

These are passed in the Task prompt that spawns this agent:

- **Site name / URL** — The specific site to search (e.g. "r/productivity", "Amazon reviews for X", "Quora topic Y")
- **Persona** — Who the ideal customer is
- **Product** — What's being sold
- **Problems** — What problems the product solves
- **Search focus** — What to look for (e.g. "fears and frustrations about productivity tools" or "identity and self-perception quotes")
- **Output file path** — Where to write results (e.g. `{output_dir}/02-site-reddit-productivity.md`)
- **Text fragment reference** — Path to `text-fragments.md` for URL formatting rules

## Search Procedure

1. **Search the specified site** for conversations relevant to the persona's problems and
   desires. Use web search queries targeted at the site (e.g. `site:reddit.com/r/productivity "tried everything"`).

2. **Focus on recent content** — posts and comments from the last 6 months when possible.

3. **Extract raw, word-for-word quotes** preserving all slang, typos, and emotional intensity.
   Sanitized quotes are useless for copy. Look for quotes that reveal:
   - What customers fear, want, believe, feel frustrated by
   - How they describe their problems in their own words
   - What triggered them to seek solutions
   - How they compare alternatives
   - What objections they raise
   - What brings them joy or relief

4. **Aim for 15-25 quotes per site.** Quality over quantity — each quote should reveal
   something meaningful about the persona's psychology. If a site is thin on relevant
   content, collect what you can and note the limitation.

## Quote Format

Record each quote with all of the following fields:

```
1. "Exact verbatim quote text here." — {author}, [{source name}]({source URL with text fragment}) ({Mon D, YYYY})
   Context: {brief tag — what the quote is about}
```

- **Verbatim text** — Word-for-word as posted. Preserve slang, typos, emotion, emphasis.
- **Author** — Username or handle (e.g. `u/habithacker`). Write "Anonymous" if not visible.
- **Source** — Markdown link with a **text fragment URL**: `[display name](URL#:~:text=quoted%20text)`.
  Read the text fragment reference file (path provided in your Task prompt) for the full syntax
  and URL-encoding rules. The text fragment should use the quote text (or a distinctive portion
  of it) so the browser scrolls to and highlights the quoted passage when clicked. For quotes
  under ~100 characters, use the full quote text. For longer quotes, use the range syntax
  (`text=first%20few%20words,last%20few%20words`).
- **Date** — Formatted as `Mon D, YYYY` (e.g. `Jan 3, 2025`). If the date is not visible on
  the page, check the Wayback Machine (web.archive.org) to find when the content was first
  captured. Write `Date Unknown` if no date can be determined.
- **Context tag** — A brief phrase describing what the quote is about (e.g. "frustration with
  onboarding complexity", "comparing alternatives to Notion").

## Incremental Writing

**After each web search that yields quotes, rewrite the output file with ALL quotes found
so far.** This is critical — if the agent hits context limits or fails partway through,
partial results are preserved in the file.

Do not accumulate all quotes in memory and write once at the end. Write after every
productive search.

## Verification

Before finalizing a quote:

1. Re-visit the source URL and confirm the quote actually appears on the page.
2. If the quote cannot be found at the cited URL, discard it and find a real replacement.
3. Do not guess or reconstruct quotes from memory — every quote in the output must exist
   verbatim at its cited source.

## Output File Format

Write the output file with this structure:

```
# Quotes from {site name}

**Search date:** {today's date}
**Quote count:** {number}
**Search focus:** {what was searched for}

---

1. "I've tried every app and nothing sticks." — u/username, [r/subreddit](https://reddit.com/r/productivity/abc123#:~:text=I've%20tried%20every%20app%20and%20nothing%20sticks) (Mar 12, 2025)
   Context: frustration with onboarding complexity

2. "Another quote here." — Anonymous, [TrustPilot review](https://trustpilot.com/review/example#:~:text=Another%20quote%20here) (Date Unknown)
   Context: comparing alternatives

...
```

Include a brief note at the end if the site had limited relevant content or if any quotes
could not be verified.
