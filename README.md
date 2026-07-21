# SciencePedia Knowledge Hierarchy

A structured extraction of the full topic hierarchy from [Bohrium SciencePedia](https://www.bohrium.com/en/sciencepedia): **47,143 topics** across **238 courses** in **9 domains** (Physics, Applied Mathematics, Chemistry, Biology, Mathematics, Computational Science, Engineering, Astronomy, Medicine), each broken down as Domain → Level → Course → Category → Chapter → Topic.

**Live page:** see the repo's GitHub Pages URL (enabled in repo settings).

## Files

- `index.html` / `sciencepedia_hierarchy.html` — interactive, collapsible hierarchy browser with a live search filter and a per-chapter "✨ Reading list" feature (see below). Same file, `index.html` is what GitHub Pages serves at the root.
- `sciencepedia_hierarchy.md` — the full hierarchy as a nested Markdown outline.
- `sciencepedia_hierarchy.txt` — the full hierarchy as plain indented text.

## The "✨ Reading list" feature

Click the ✨ button next to any **chapter** (3,990 total — one level up from individual topics) to get:
- A **detailed plain-language overview** of everything the chapter covers, referencing its actual topics (via the Anthropic Claude API).
- **Real, verifiable related papers**, looked up live by chapter title via the free [OpenAlex](https://openalex.org) scholarly API (falling back to the course title if the chapter title has no direct match) — no key required for this part.
- **AI-suggested further reading** — 5-8 well-known textbooks/resources per chapter (via Claude), clearly labeled as unverified; confirm titles before citing.

This is scoped to chapters rather than individual topics: chapter titles read like real textbook section titles (so the paper search is much more relevant), and a chapter's worth of further reading is more useful than one per narrow topic.

Every chapter also always shows (no key, no click needed):
- A **Scholar** link — opens a Google Scholar search for that chapter, scoped with its course and domain name for context.
- An **OpenAlex** link — opens OpenAlex's own works search, filtered by chapter title *and* field-of-study (e.g. Physics vs. Mathematics), so a generic chapter name like "Geometry" doesn't collide across domains.

Papers returned in-page from OpenAlex include their **citation count**, plus a "who cites it" link to see later work that references them.

### On search relevance

OpenAlex's `title.search` requires the query terms to appear in the paper's own title, and results are additionally constrained to match the chapter's domain (Physics, Chemistry, etc.) via OpenAlex's field-of-study taxonomy — this avoids the two failure modes of naive keyword search: (1) tangential full-text matches from completely unrelated fields, and (2) same-word-different-field collisions (e.g. "oscillatory motion" in biomechanics vs. classical mechanics, "geometry" in physics vs. pure math). If no in-domain title match exists, it falls back to a domain-unfiltered search, then a stripped/simplified title, then the course title, before giving up and showing "no closely matching papers."

### About the API key

The explanation and AI-reading-list features call the Anthropic API **directly from your browser**, using an API key **you provide yourself** via the "⚙ API Settings" button.

- The key is stored **only in your browser's local storage** (`localStorage`), scoped to this page.
- It is **never** sent to any server other than `api.anthropic.com`, and **never** written into this repository or any file.
- Results are cached in your browser's local storage after the first lookup, so repeat views don't re-call the API.
- Get a key at [console.anthropic.com](https://console.anthropic.com/).

If you don't set a key, the real-paper lookups (OpenAlex) still work — only the AI explanation/reading-list portion is skipped.

## Provenance

Extracted via browser automation against Bohrium's internal (WAF-protected) `wiki_v2` endpoints, verified topic-by-topic against the site's own per-course counts (zero mismatches across all 238 courses). See commit history / conversation for extraction methodology.

Generated with [Claude Code](https://claude.com/claude-code).
