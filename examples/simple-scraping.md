# Simple Scraping

Goal:
Fetch one page without opening a browser session.

Prerequisite:

```bash
export GOLOGIN_WEB_UNLOCKER_API_KEY="your_web_unlocker_key"
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
