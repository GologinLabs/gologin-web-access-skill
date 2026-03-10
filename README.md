# Gologin Web Access Skill

## Overview

Gologin Web Access Skill gives AI agents and external developers one consistent interface for web scraping and browser automation through Gologin infrastructure:

- reading the web through Gologin Web Unlocker
- interacting with the web through Gologin Cloud Browser

Architecture:

```text
agent
-> skill
-> gologin-web-access CLI
-> Web Unlocker API / Gologin Cloud Browser
```

The skill keeps the current model intact:

- Firecrawl-style delegation: agent -> skill -> CLI -> API
- Agent Browser-style interaction: snapshot -> refs -> deterministic actions

It does not implement scraping or browser automation itself. It delegates to:

- CLI: `gologin-web-access`
- Repository: [GologinLabs/gologin-web-access](https://github.com/GologinLabs/gologin-web-access)

## Capabilities

- Read rendered HTML with `scrape_url`
- Extract readable markdown with `scrape_markdown`
- Extract plain text with `scrape_text`
- Extract structured metadata with `scrape_json`
- Batch multiple pages with `batch_scrape`
- Open and manage live browser sessions with `browser_open`, `browser_sessions`, and `browser_current`
- Interact with live pages through `browser_snapshot`, `browser_click`, and `browser_type`
- Capture artifacts with `browser_screenshot`
- End sessions with `browser_close`

## Installation

Option 1: install globally

```bash
npm install -g gologin-web-access
```

Option 2: run with `npx`

```bash
npx gologin-web-access scrape-markdown https://example.com
```

## Setup

Set environment variables:

```bash
export GOLOGIN_WEB_UNLOCKER_API_KEY="your_web_unlocker_key"
export GOLOGIN_CLOUD_TOKEN="your_cloud_token"
export GOLOGIN_DEFAULT_PROFILE_ID="optional_profile_id"
```

Setup rules:

- Scraping commands require `GOLOGIN_WEB_UNLOCKER_API_KEY`
- Browser commands require `GOLOGIN_CLOUD_TOKEN`
- `GOLOGIN_DEFAULT_PROFILE_ID` is optional and recommended when you want a stable browser identity

## Quickstart

Read a page:

```bash
gologin-web-access scrape-markdown https://example.com
```

Start browser interaction:

```bash
gologin-web-access open https://example.com
gologin-web-access snapshot
```

Typical snapshot output:

```text
session=s1 url=https://example.com/
- heading "Example Domain" [ref=@e1]
- link "More information" [ref=@e2]
```

Use the returned ref for the next action:

```bash
gologin-web-access click "@e2"
```

## Tool Selection Guide

| Task | Use |
| --- | --- |
| Read page content | Scraping |
| Extract article text | Scraping |
| Pull headings and links | Scraping |
| Batch several URLs | Scraping |
| Click buttons | Browser |
| Fill forms | Browser |
| Login flows | Browser |
| Capture screenshots | Browser |
| Inspect active browser sessions | Browser |

## Tool Groups

### Scraping

- `scrape_url`
- `scrape_markdown`
- `scrape_text`
- `scrape_json`
- `batch_scrape`

### Browser

- `browser_open`
- `browser_snapshot`
- `browser_click`
- `browser_type`
- `browser_screenshot`
- `browser_close`
- `browser_sessions`
- `browser_current`

The skill tool names stay stable even when the underlying CLI commands are shorter. See [`tools.md`](./tools.md) for the exact mapping.

## Examples

- [`examples/simple-scraping.md`](./examples/simple-scraping.md): minimal single-page scraping
- [`examples/scrape-only.md`](./examples/scrape-only.md): scrape-first pattern for read-only tasks

## Workflows

- [`workflows/browser-ref-loop.md`](./workflows/browser-ref-loop.md): the canonical snapshot -> ref -> action loop
- [`workflows/hybrid-read-then-interact.md`](./workflows/hybrid-read-then-interact.md): start stateless, escalate to browser when needed
- [`workflows/login-and-navigate-dashboard.md`](./workflows/login-and-navigate-dashboard.md): login flow with snapshot refs
- [`workflows/form-interaction-and-results.md`](./workflows/form-interaction-and-results.md): form submission and result extraction
- [`workflows/scrape-multiple-pages.md`](./workflows/scrape-multiple-pages.md): batch scraping flow
- [`workflows/extract-article-content.md`](./workflows/extract-article-content.md): article extraction flow
