# Simple Scraping

Goal:
Fetch one page without opening a browser session.

Prerequisite:

```bash
export GOLOGIN_SCRAPING_API_KEY="your_scraping_api_key"
```

Commands:

```bash
gologin-web-access scrape-markdown "https://example.com"
```

```bash
gologin-web-access scrape-json "https://example.com"
```

Use this example when:

- the task is read-only
- a browser session is unnecessary
- markdown or structured metadata is enough
