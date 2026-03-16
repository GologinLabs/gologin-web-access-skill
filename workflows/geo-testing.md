# Geo Testing

Use this when the user needs readable output or screenshots from a geo-sensitive page through GoLogin infrastructure.

## Pattern

```bash
gologin-web-access read https://example.com/location-page
gologin-web-access scrape-screenshot https://example.com/location-page ./artifacts/location.png
```

## Notes

- Use `read` first for content.
- Use screenshot capture when interactive charts, maps, or visual evidence matter.
- If Cloud Browser slots are exhausted and the task can run locally, route to `gologin-local-agent-browser` instead of grinding on cloud retries.
