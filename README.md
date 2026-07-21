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
