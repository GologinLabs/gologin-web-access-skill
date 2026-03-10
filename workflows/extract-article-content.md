# Workflow: Extract Article Content

Goal:
Extract readable content from a page without opening a browser session.

Tool choice:

- Use `scrape_markdown` when you want a readable article body.
- Use `scrape_json` when you also want headings and links.

Commands:

```bash
gologin-web-access scrape-markdown "https://example.com/blog/launch-post"
```

```bash
gologin-web-access scrape-json "https://example.com/blog/launch-post"
```

Expected pattern:

- first command returns markdown
- second command returns structured JSON with title, description, headings, and links

Why this flow:

- no clicks are required
- no browser session is required
- Web Unlocker is the simplest path
