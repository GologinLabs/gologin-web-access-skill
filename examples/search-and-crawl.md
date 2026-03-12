# Search And Crawl

Use search-first discovery when the user starts from a topic instead of a known URL.

```bash
gologin-web-access search "gologin antidetect browser" --limit 5 --source auto
gologin-web-access map https://gologin.com --limit 25 --max-depth 2
gologin-web-access crawl https://gologin.com/docs --format markdown --limit 20 --max-depth 2
```

Use this pattern when:

- the user starts from a query
- the target site should be discovered before crawling
- the task is read-only and does not require a live browser session
