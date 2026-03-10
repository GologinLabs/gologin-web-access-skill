# Workflow: Form Interaction And Results

Goal:
Fill a search form, submit it, inspect the results snapshot, and save a screenshot.

Prerequisites:

```bash
export GOLOGIN_CLOUD_TOKEN="gl_..."
export GOLOGIN_DEFAULT_PROFILE_ID="profile_123"
```

Commands:

```bash
gologin-web-access open "https://example.com/search"
gologin-web-access snapshot
```

Assume the snapshot includes:

```text
- input "Search" [ref=@e1]
- button "Submit" [ref=@e2]
```

Continue:

```bash
gologin-web-access type "@e1" "pricing"
gologin-web-access click "@e2"
gologin-web-access snapshot
gologin-web-access screenshot "/tmp/search-results.png"
gologin-web-access close
```

Result extraction pattern:

- read result headings, links, and text from the new snapshot
- use the latest refs only
- if the page changed after submit, never reuse the old refs
