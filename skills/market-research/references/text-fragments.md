# Text Fragment URLs

When collecting quotes alongside source URLs, append a **Text Fragment** directive so the
link scrolls to and highlights the quoted text in the reader's browser.

## Syntax

```
https://example.com/page#:~:text=encoded%20text%20here
```

The fragment directive `#:~:text=` goes after the URL. The text content must be URL-encoded
(spaces become `%20`, special characters like `$` become `%24`, etc.).

### Range syntax for long quotes

If the quoted text is longer than ~100 characters, use the range syntax with just the
first few words and last few words:

```
#:~:text=first%20few%20words,last%20few%20words
```

The browser will highlight everything from `textStart` to `textEnd`.

### URLs that already have a fragment

If the source URL already contains a `#` fragment (e.g. `page#section-id`), append the
text directive after it using the `:~:` delimiter:

```
https://example.com/page#section-id:~:text=quoted%20text
```

## Rules

1. **Only add text fragments when you have a specific quote from the page.** If a URL is
   a general reference with no specific quoted passage, leave it as-is.

2. **Use the quote text itself** (or a distinctive substring of it) as the text fragment.
   Pick the most unique portion — avoid generic phrases that might match elsewhere on the page.

3. **Keep fragments short.** Aim for under 100 characters of text in the fragment. For
   longer quotes, use the `textStart,textEnd` range syntax with ~4-8 words from the
   beginning and ~4-8 words from the end.

4. **URL-encode the text.** Spaces become `%20`. Encode special characters:
   `$` → `%24`, `&` → `%26`, `+` → `%2B`, `,` → `%2C` (but commas that separate
   `textStart` from `textEnd` are NOT encoded), `/` → `%2F`, `?` → `%3F`,
   `#` → `%23`, `=` → `%3D`, `@` → `%40`.

5. **Preserve the full original URL** (including any existing query parameters or fragments)
   before appending the text directive.

## Examples

Short quote — use full text:
```
"I tried everything and nothing stuck."
→ https://reddit.com/r/productivity/abc123#:~:text=I%20tried%20everything%20and%20nothing%20stuck
```

Long quote — use range syntax:
```
"After three months of trying every productivity app on the market, I finally realized that the tool wasn't the problem — my entire approach to task management was broken from the start."
→ https://reddit.com/r/productivity/abc123#:~:text=After%20three%20months%20of%20trying,was%20broken%20from%20the%20start
```

URL with existing fragment:
```
"The onboarding process took forever."
→ https://example.com/review#user-reviews:~:text=The%20onboarding%20process%20took%20forever
```

## Markdown Link Format

In markdown output, the text fragment URL goes inside the link parentheses as usual:

```
[r/productivity](https://reddit.com/r/productivity/abc123#:~:text=I%20tried%20everything)
```
