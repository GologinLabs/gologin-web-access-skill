# Workflow: Scrape Multiple Pages

Goal:
Extract several pages in one stateless pass.

Prerequisite:

```bash
export GOLOGIN_WEB_UNLOCKER_API_KEY="wu_..."
```

Command:

```bash
gologin-web-access batch-scrape \
  "https://example.com/docs/start" \
  "https://example.com/docs/api" \
  "https://example.com/docs/pricing" \
  --format markdown
```

Expected pattern:

- returns one JSON array
- each item contains `url`, `ok`, `format`, and either `output` or `error`

Why this flow:

- the task is read-only
- batching is faster than opening several browser sessions
- markdown output is easier for downstream analysis
