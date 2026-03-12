# Search, Discover, And Scrape

This workflow is the read-only path for tasks that begin from a topic or keyword.

## Pattern

1. Run `gologin-web-access search "<query>" --source auto` to discover likely targets.
2. Pick the most relevant URL from the results.
3. Use `map` if the task needs internal site discovery before extraction.
4. Use `crawl` for multi-page read-only extraction.
5. Use `scrape-markdown`, `scrape-text`, or `extract` for the final output shape.

## Example

```bash
gologin-web-access search "gologin antidetect browser" --limit 5 --source auto
gologin-web-access map https://gologin.com --limit 20 --max-depth 2
gologin-web-access scrape-markdown https://gologin.com/docs
```

Use `search-browser` instead if the workflow should begin from a live browser-visible SERP.
