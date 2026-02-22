# Codicent Status

System status page for [codicent.com](https://codicent.com), served via GitHub Pages at **https://izaxon.github.io/codicent-status/**.

## How it works

A GitHub Actions workflow (`.github/workflows/update-status.yml`) runs every 5 minutes and:

1. Hits the `https://codicent.com/health` endpoint
2. Maps the HTTP response to a status level (Operational / Degraded Performance / Partial Outage / Major Outage)
3. If the status has **changed**, updates `status.json` and commits it  no spurious commits when everything is healthy

The status page (`index.html`) fetches `status.json` at load time and auto-refreshes every 60 seconds client-side.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Status page (self-contained, no build step) |
| `status.json` | Current status + incident history (updated by workflow) |
| `.github/workflows/update-status.yml` | Cron job  polls health endpoint, updates `status.json` |

## Custom domain

To serve from `status.codicent.com`, add a `CNAME` file containing `status.codicent.com` and configure a DNS CNAME record pointing to `izaxon.github.io`.