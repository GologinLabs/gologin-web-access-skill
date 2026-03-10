# Hybrid Read Then Interact

Use this workflow when the task starts as content extraction but may need a browser later.

## Sequence

1. Start with `scrape_json`, `scrape_markdown`, or `scrape_text`.
2. Inspect whether the task can finish from stateless content alone.
3. Switch to `browser_open` when the task requires login, navigation, forms, or session continuity.
4. Move into the snapshot and ref loop.
5. Save artifacts with `browser_screenshot` if needed.
6. Close the session when done.

## Why This Exists

- scraping is cheaper and simpler for read-only work
- browser automation is stronger for interactive work
- the combined skill lets the agent move between both modes without changing providers
