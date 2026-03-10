# Scrape-Only

Use this example when the page can be read without a browser session.

## Decision

Choose scraping if:

- the task is read-only
- the page does not require interaction
- the site does not require session continuity

## Commands

```bash
gologin-web-access scrape-text "https://example.com/docs/start"
gologin-web-access scrape-json "https://example.com/docs/start"
gologin-web-access batch-scrape "https://example.com/docs/start" "https://example.com/docs/api" --format markdown
```

## Sequence

1. Choose the smallest output format that fits the task.
2. Run `scrape_url` for raw HTML.
3. Run `scrape_markdown` for article-like content.
4. Run `scrape_text` for analysis-friendly plain text.
5. Run `scrape_json` for metadata and links.
6. Run `batch_scrape` for multiple URLs.

## Rule

Do not open a browser unless the scrape result is insufficient for the job.
