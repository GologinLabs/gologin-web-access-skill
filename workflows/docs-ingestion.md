# Docs Ingestion

Use this when the user wants a docs page, article, or product documentation section pulled into clean readable text.

## Pattern

```bash
gologin-web-access read https://docs.browserbase.com/features/contexts
gologin-web-access crawl https://docs.browserbase.com --format text --only-main-content --limit 20 --max-depth 2
```

## Notes

- Start with `read` for one page.
- Use `crawl --only-main-content` for one docs section or site.
- If `scrape-json` warns that the result looks client-rendered or incomplete across repeated pages, escalate to a browser-backed path or local GoLogin runtime.
