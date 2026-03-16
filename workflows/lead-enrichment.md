# Lead Enrichment

Use this when the user already has a list of company, pricing, or contact URLs and wants the same extraction schema on each page.

## Pattern

```bash
gologin-web-access batch-extract https://example.com https://example.org \
  --schema ./schema.json \
  --summary \
  --output ./artifacts/leads.json
```

## Notes

- Prefer `batch-extract` over ad-hoc loops in the shell.
- Keep schemas deterministic and narrow.
- If a page is JS-heavy, use `--source auto` or `--source browser`.
