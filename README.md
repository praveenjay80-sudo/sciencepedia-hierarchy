# SciencePedia Knowledge Hierarchy

A structured extraction of the full topic hierarchy from [Bohrium SciencePedia](https://www.bohrium.com/en/sciencepedia): **47,143 topics** across **238 courses** in **9 domains** (Physics, Applied Mathematics, Chemistry, Biology, Mathematics, Computational Science, Engineering, Astronomy, Medicine), each broken down as Domain → Level → Course → Category → Chapter → Topic.

**Live page:** see the repo's GitHub Pages URL (enabled in repo settings).

## Files

- `index.html` / `sciencepedia_hierarchy.html` — interactive, collapsible hierarchy browser with a live search filter and a per-chapter "✨ Reading list" feature (see below). Same file, `index.html` is what GitHub Pages serves at the root.
- `sciencepedia_hierarchy.md` — the full hierarchy as a nested Markdown outline.
- `sciencepedia_hierarchy.txt` — the full hierarchy as plain indented text.

## The "✨ Reading list" feature

Click the ✨ Reading list button next to any **chapter** (3,990 total — one level up from individual topics) to get, entirely from the Anthropic Claude API:
- A **detailed plain-language overview** of everything the chapter covers, grounded in its actual topic list.
- A **reading list** of 5-8 well-known textbooks/resources, each with a note on why it's relevant, plus a "verify on Scholar" link per item so you can confirm it's real before relying on it.

This is scoped to chapters rather than individual topics: chapter titles read like real textbook section titles, and a chapter's worth of further reading is more useful than one per narrow topic.

**Why this is fully AI-generated rather than live-searched:** an earlier version also queried the free [OpenAlex](https://openalex.org) scholarly API live for "real, verifiable" papers on every click. That was removed - OpenAlex enforces a very small per-client daily request budget on its public API (observed `Retry-After` once exhausted: **~13 hours**), so most visitors would just see a rate-limit error instead of results most of the time. Rather than a feature that mostly fails, every chapter still always shows two static links that need no API call and never rate-limit:
- A **Scholar** link — opens a Google Scholar search for that chapter, scoped with its course and domain for context.
- An **OpenAlex** link — opens OpenAlex's own works search, filtered by chapter title *and* field-of-study (e.g. Physics vs. Mathematics), so a generic chapter name like "Geometry" doesn't collide across domains.

Use those to check real sources yourself; treat the AI reading list as a starting point, not a citation.

### About the API key

The chapter-overview and reading-list feature calls the Anthropic API **directly from your browser**, using an API key **you provide yourself** via the "⚙ API Settings" button.

- The key is stored **only in your browser's local storage** (`localStorage`), scoped to this page.
- It is **never** sent to any server other than `api.anthropic.com`, and **never** written into this repository or any file.
- Results are cached in your browser's local storage after the first lookup, so repeat views don't re-call the API.
- Get a key at [console.anthropic.com](https://console.anthropic.com/).

Without a key, the ✨ button won't produce an overview/reading list, but the Scholar/OpenAlex links on every chapter work regardless.

## Performance: lazy topic rendering

Earlier versions built all 47,143 topics' `<li>` markup into the page on load (~94,000 DOM nodes total), which was slow enough to trigger the browser's "Page Unresponsive" warning. Topic data now lives in a compact JS array (`TOPIC_DATA`) instead of inline HTML, and each chapter's topic list is only rendered into the DOM the moment that chapter is actually opened (or matched by a search) — cutting the up-front DOM to ~5,000 skeleton nodes (domains/levels/courses/categories/chapters only). Search still works instantly across all 47,143 topics because it matches against `TOPIC_DATA` directly rather than scanning the DOM, and only renders the chapters that actually match.

## Provenance

Extracted via browser automation against Bohrium's internal (WAF-protected) `wiki_v2` endpoints, verified topic-by-topic against the site's own per-course counts (zero mismatches across all 238 courses). See commit history / conversation for extraction methodology.

Generated with [Claude Code](https://claude.com/claude-code).
