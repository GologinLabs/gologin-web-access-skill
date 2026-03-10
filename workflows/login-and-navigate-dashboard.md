# Workflow: Login And Navigate Dashboard

Goal:
Log into a site, land on the dashboard, capture a screenshot, and close the session.

Prerequisites:

```bash
export GOLOGIN_CLOUD_TOKEN="gl_..."
export GOLOGIN_DEFAULT_PROFILE_ID="profile_123"
export APP_EMAIL="user@example.com"
export APP_PASSWORD="secret"
```

Commands:

```bash
gologin-web-access open "https://app.example.com/login"
```

```bash
gologin-web-access snapshot
```

Assume the snapshot includes:

```text
- input "Email" [ref=@e1]
- input "Password" [ref=@e2]
- button "Sign in" [ref=@e3]
```

Continue:

```bash
gologin-web-access type "@e1" "$APP_EMAIL"
gologin-web-access type "@e2" "$APP_PASSWORD"
gologin-web-access click "@e3"
gologin-web-access snapshot
gologin-web-access screenshot "/tmp/dashboard.png"
gologin-web-access close
```

Why this flow:

- the site requires a real browser session
- the flow needs typing and clicking
- each interaction depends on the latest snapshot refs
