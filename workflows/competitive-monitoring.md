# Competitive Monitoring

Use this when the user wants repeated checks on pricing, features, policy, or landing pages from one or more competitors.

## Pattern

```bash
gologin-web-access batch-change-track https://example.com/pricing https://example.com/features \
  --format markdown \
  --summary \
  --output ./artifacts/watchlist.json
```

## Notes

- Prefer `batch-change-track` when the URLs are already known.
- Use `map` or `crawl` only to discover the initial watchlist.
- Save artifacts with `--output` instead of parsing stdout later.
