# Tool Contracts

All tools in this skill are thin wrappers over the published `gologin-web-access` CLI.

Canonical CLI:

```bash
gologin-web-access <command> ...
```

Repository:

[GologinLabs/gologin-web-access](https://github.com/GologinLabs/gologin-web-access)

## Summary

| Skill tool | CLI command | Requires | Returns |
| --- | --- | --- | --- |
| `scrape_url` | `scrape` | `GOLOGIN_WEB_UNLOCKER_API_KEY` | Rendered HTML |
| `read_page` | `read` | `GOLOGIN_WEB_UNLOCKER_API_KEY` or `GOLOGIN_CLOUD_TOKEN` when `--source browser` is forced | Main-content-first html, markdown, or text |
| `scrape_markdown` | `scrape-markdown` | `GOLOGIN_WEB_UNLOCKER_API_KEY` or `GOLOGIN_CLOUD_TOKEN` when `--source browser` is forced | Markdown, with `--source auto|unlocker|browser` |
| `scrape_text` | `scrape-text` | `GOLOGIN_WEB_UNLOCKER_API_KEY` or `GOLOGIN_CLOUD_TOKEN` when `--source browser` is forced | Plain text, with `--source auto|unlocker|browser` |
| `scrape_json` | `scrape-json` | `GOLOGIN_WEB_UNLOCKER_API_KEY` | Structured JSON with heading levels, render source, and retry metadata |
| `batch_scrape` | `batch-scrape` | `GOLOGIN_WEB_UNLOCKER_API_KEY` | JSON array with per-URL status, optional summary, structured envelopes for `--format json`, and optional main-content extraction |
| `batch_extract` | `batch-extract` | `GOLOGIN_WEB_UNLOCKER_API_KEY` or `GOLOGIN_CLOUD_TOKEN` when `--source browser` is forced | JSON array with one structured extraction result per URL, or a saved output file path |
| `crawl_site` | `crawl` | `GOLOGIN_WEB_UNLOCKER_API_KEY` | Site crawl results with `status: ok|partial|failed`, and optional main-content extraction for html, markdown, and text output |
| `batch_track_changes` | `batch-change-track` | `GOLOGIN_WEB_UNLOCKER_API_KEY` | JSON array with one watchlist-style change result per URL, or a saved output file path |
| `browser_open` | `open` | `GOLOGIN_CLOUD_TOKEN` | Session summary |
| `browser_snapshot` | `snapshot` | `GOLOGIN_CLOUD_TOKEN` | Snapshot with refs |
| `browser_click` | `click` | `GOLOGIN_CLOUD_TOKEN` | Action status |
| `browser_type` | `type` | `GOLOGIN_CLOUD_TOKEN` | Action status |
| `browser_screenshot` | `screenshot` | `GOLOGIN_CLOUD_TOKEN` | Screenshot path |
| `browser_close` | `close` | `GOLOGIN_CLOUD_TOKEN` | Close status |
| `browser_sessions` | `sessions` | `GOLOGIN_CLOUD_TOKEN` | Session list |
| `browser_current` | `current` | `GOLOGIN_CLOUD_TOKEN` | Current session summary |

## scrape_url

Purpose:
Read rendered HTML for one page through Web Unlocker.

CLI:

```bash
gologin-web-access scrape "<url>"
```

Returns:
Rendered HTML on stdout.

Use when:
Raw HTML or original page structure is needed.

## scrape_markdown

Purpose:
Read a page as markdown through Web Unlocker.

CLI:

```bash
gologin-web-access scrape-markdown "<url>" [--source auto|unlocker|browser]
```

Returns:
Markdown on stdout.

Use when:
Readable article or documentation output is needed.

## read_page

Purpose:
Read the main content of a docs page or article with the least friction.

CLI:

```bash
gologin-web-access read "<url>" [--format text|markdown|html] [--source auto|unlocker|browser]
```

Returns:
Readable page content on stdout, using the most likely article/docs block.

Use when:
The user simply wants you to read and summarize one page without debugging rendering paths by hand.

## scrape_text

Purpose:
Read a page as plain text through Web Unlocker.

CLI:

```bash
gologin-web-access scrape-text "<url>" [--source auto|unlocker|browser]
```

Returns:
Plain text on stdout.

Use when:
Stripped text is needed for downstream analysis.

## scrape_json

Purpose:
Read structured page metadata through Web Unlocker.

CLI:

```bash
gologin-web-access scrape-json "<url>" [--fallback browser]
```

Returns:

```json
{
  "url": "https://example.com",
  "status": 200,
  "renderSource": "unlocker",
  "fallbackAttempted": false,
  "fallbackUsed": false,
  "request": {
    "attemptCount": 1,
    "retryCount": 0,
    "attempts": [
      {
        "attempt": 1,
        "status": 200,
        "retriable": false
      }
    ]
  },
  "data": {
    "title": "Example Domain",
    "description": null,
    "canonical": "https://example.com/",
    "meta": {},
    "headings": ["Example Domain"],
    "headingsByLevel": {
      "h1": ["Example Domain"],
      "h2": [],
      "h3": [],
      "h4": [],
      "h5": [],
      "h6": []
    },
    "links": [
      {
        "text": "More information",
        "href": "https://www.iana.org/domains/example"
      }
    ]
  }
}
```

Use when:
Metadata, headings, and extracted links are enough.

## batch_scrape

Purpose:
Read multiple pages in one CLI call through Web Unlocker.

CLI:

```bash
gologin-web-access batch-scrape "<url-1>" "<url-2>" --format markdown --retry 3 --backoff-ms 2000 --summary
```

Returns:

```json
[
  {
    "url": "https://example.com/a",
    "ok": true,
    "format": "json",
    "output": {
      "url": "https://example.com/a",
      "status": 200,
      "renderSource": "unlocker",
      "fallbackAttempted": false,
      "fallbackUsed": false,
      "request": {
        "attemptCount": 1,
        "retryCount": 0,
        "attempts": [
          {
            "attempt": 1,
            "status": 200,
            "retriable": false
          }
        ]
      },
      "data": {
        "title": "Page A",
        "description": null,
        "canonical": null,
        "meta": {},
        "headings": [],
        "headingsByLevel": {
          "h1": [],
          "h2": [],
          "h3": [],
          "h4": [],
          "h5": [],
          "h6": []
        },
        "links": []
      }
    }
  },
  {
    "url": "https://example.com/b",
    "ok": false,
    "format": "json",
    "error": "Web Unlocker request failed with status 503.",
    "status": 503,
    "request": {
      "attemptCount": 2,
      "retryCount": 1,
      "attempts": [
        {
          "attempt": 1,
          "status": 429,
          "error": "Web Unlocker request failed with status 429.",
          "retriable": true
        },
        {
          "attempt": 2,
          "status": 503,
          "error": "Web Unlocker request failed with status 503.",
          "retriable": false
        }
      ]
    }
  }
]
```

Use when:
Several stateless URLs should be fetched in one pass.

Notes:
Add `--only-main-content` for html, markdown, or text batch runs when the goal is readable docs/article content rather than full page chrome.

## batch_extract

Purpose:
Apply one selector schema across many known URLs.

CLI:

```bash
gologin-web-access batch-extract "<url-1>" "<url-2>" --schema ./schema.json --summary --output ./artifacts/extract.json
```

Returns:
JSON array with one structured extraction result per URL, including fallback and request metadata, or the written output path when `--output` is used.

Use when:
You already know the target URLs and want deterministic enrichment rather than generic page reading.

## crawl_site

Purpose:
Traverse multiple pages from one site through Web Unlocker.

CLI:

```bash
gologin-web-access crawl "<url>" --format text --only-main-content
```

Returns:
JSON with per-page crawl output and overall `status`.

Use when:
You need multi-page stateless extraction, and `--only-main-content` helps when the useful content is inside a specific article/docs region rather than the full page shell.

## batch_track_changes

Purpose:
Check many known pages for `new`, `same`, or `changed` results in one pass.

CLI:

```bash
gologin-web-access batch-change-track "<url-1>" "<url-2>" --format text --summary --output ./artifacts/watchlist.json
```

Returns:
JSON array with one change result per URL, plus an optional summary line on stderr, or the written output path when `--output` is used.

Use when:
You have a watchlist of pages to monitor for changes without building a crawler.

## browser_open

Purpose:
Start or reuse a Cloud Browser session for a URL.

CLI:

```bash
gologin-web-access open "<url>"
```

Optional profile:

```bash
gologin-web-access open "<url>" --profile "<profile-id>"
```

Returns:

```text
session=s1 url=https://example.com
```

Use when:
A real browser session is required for state, login, navigation, or interaction.

## browser_snapshot

Purpose:
Capture the current page state and assign deterministic refs for the next action.

CLI:

```bash
gologin-web-access snapshot
```

Returns:

```text
session=s1 url=https://example.com/
- heading "Example Domain" [ref=@e1]
- link "More information" [ref=@e2]
```

Use when:
The next clickable or typable target must come from the current page.

Rule:
All ref-based browser actions must use the latest snapshot.

## browser_click

Purpose:
Click a snapshot ref.

CLI:

```bash
gologin-web-access click "@e2"
```

Returns:

```text
click target=@e2 session=s1 url=https://example.com snapshot=stale
```

Use when:
The next browser action is a click derived from the latest snapshot.

Rule:
If the command returns `snapshot=stale`, run `browser_snapshot` before the next ref-based step.

## browser_type

Purpose:
Type into a snapshot ref.

CLI:

```bash
gologin-web-access type "@e1" "hello world"
```

Returns:

```text
type target=@e1 session=s1 url=https://example.com/search snapshot=stale
```

Use when:
The target field is already identified in the latest snapshot.

## browser_screenshot

Purpose:
Save a screenshot from the current Cloud Browser session.

CLI:

```bash
gologin-web-access screenshot "/absolute/path/to/page.png"
```

Returns:

```text
screenshot=/absolute/path/to/page.png session=s1
```

Use when:
A visual artifact of the page state is needed.

## browser_close

Purpose:
End the current Cloud Browser session.

CLI:

```bash
gologin-web-access close
```

Returns:

```text
closed session=s1
```

Use when:
The browser flow is complete and the session should be cleaned up.

## browser_sessions

Purpose:
List all active daemon-backed browser sessions.

CLI:

```bash
gologin-web-access sessions
```

Returns:

```text
* session=s1 url=https://example.com snapshot=fresh
- session=s2 url=https://example.org snapshot=stale
```

Use when:
The agent needs to inspect or choose among multiple active browser sessions.

## browser_current

Purpose:
Show the current daemon-backed browser session.

CLI:

```bash
gologin-web-access current
```

Returns:

```text
session=s1 url=https://example.com snapshot=fresh
```

Use when:
The agent needs the active session summary before taking the next browser step.
