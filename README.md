# Fulcorum

Promotional site for Fulcorum — AI enablement for measurable ROI in software engineering and leadership.

Single-page app (`index.html`), hash-routed between **Home** and **Events**. No build step, no dependencies. Served by GitHub Pages from `main`.

## Adding events

Edit `events.json` — an array of objects. Empty array shows the "no events yet" state.

```json
[
  {
    "title": "Constraint Engineering Workshop",
    "type": "Workshop",
    "date": "2026-09-18",
    "time": "9:00 AM – 4:00 PM CT",
    "location": "Austin, TX",
    "description": "Hands-on: shape your repo so agents produce work you can ship.",
    "url": "https://www.eventbrite.com/e/your-event-id"
  }
]
```

| field         | notes                                                        |
|---------------|--------------------------------------------------------------|
| `title`       | required                                                     |
| `type`        | drives the filter chips (e.g. Conference, Workshop, Roundtable, Talk) |
| `date`        | `YYYY-MM-DD` — used for the date badge and sort order        |
| `time`        | free text                                                    |
| `location`    | free text                                                    |
| `description` | free text                                                    |
| `url`         | Eventbrite registration link — renders the "Register" button |

Events sort by date automatically. Commit `events.json` to publish.

> **Eventbrite auto-pull:** a static site can't safely call Eventbrite's API from the browser (the token would be exposed, and the public event-search API was retired). To automate later, add a scheduled GitHub Action that fetches your org's events with a repo secret and writes `events.json`.

## GitHub Pages setup

1. Repo **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main` / `/ (root)`.
2. Custom domain is set via the `CNAME` file (`fulcorum.com`).
3. DNS at your registrar:
   - Apex `fulcorum.com` → four **A** records:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
     (and/or **AAAA** records for IPv6 — see GitHub Pages docs)
   - `www.fulcorum.com` → **CNAME** → `tacoda.github.io`
4. Enable **Enforce HTTPS** once the cert provisions.

## Background

The hero background is a pure-CSS/JS animated Claude Code terminal with a slow pan — no video asset required. To swap in a real screen recording later, drop an `<video>` into `.hero-bg` and hide `.term-pan`.
