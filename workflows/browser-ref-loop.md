# Browser Ref Loop

Use this workflow when the task needs browser state.

## Sequence

1. Run `browser_open`.
2. Run `browser_snapshot`.
3. Inspect the returned refs.
4. Choose the next deterministic action.
5. Run `browser_click` or `browser_type` with the latest ref.
6. If the page changed or the command returned `snapshot=stale`, run `browser_snapshot` again.
7. Repeat until the task is complete.
8. Run `browser_screenshot` if the task needs an artifact.
9. Run `browser_close`.

## Rule

Snapshot output is the only source of truth for ref-based actions.

## Example Shape

```text
- heading "Example Domain" [ref=@e1]
- link "More information" [ref=@e2]
```

Next action:

```bash
gologin-web-access click "@e2"
```
