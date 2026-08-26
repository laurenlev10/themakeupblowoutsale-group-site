# themakeupblowoutsale-group-site

Public marketing landing site served at **https://www.themakeupblowoutsale-group.com/**.

Hosts the QR-code subscribe page (`/subscribe-list/`) printed on every event door — replaces the old ClickFunnels page (deprecated 2026-05-11).

## Structure

```
docs/
  CNAME                       www.themakeupblowoutsale-group.com
  index.html                  redirect → /subscribe-list/
  subscribe-list/index.html   the QR landing page (phone-only SimpleTexting form)
  state/                      (reserved for future per-page state files)
  _assets/                    (reserved for shared images / svgs)
```

## How the form works

The page's PRIMARY source is the public events feed
`https://events.themakeupblowout.com/upcoming-events.json`, with
`https://dashboard.themakeupblowout.com/state/subscribe_target.json` as a
single-object fallback. From either it uses:
- `form_id` → the SimpleTexting webForm for the upcoming event's contact list
- `ig_reel_url` / `fb_url` / `tiktok_url` → per-event share buttons
- `city`/`state`/`start_date`/`end_date` → "Next event" pill

If both fetches fail, the form falls back to the most-recent known good `form_id`
hard-coded in the page.

> 🛑 Corrected 2026-08-26. This paragraph used to name
> `https://laurenlev10.github.io/lauren-agent-hub-data/state/subscribe_target.json`.
> That URL died in 2026-08 when `lauren-agent-hub-data` went private, which broke the
> share buttons; the page was moved to the public events feed on 2026-08-07 and the
> README was never updated. Documentation that names a dead address is how the next
> person "restores" a page to something that cannot work — the guardrail
> `consumer-repos-carry-no-dead-url` reported this line for weeks.

## Custom domain

DNS is configured at GoDaddy:
- `www.themakeupblowoutsale-group.com` → CNAME → `laurenlev10.github.io`
- `themakeupblowoutsale-group.com` (apex) → 4× A records to GitHub Pages IPs (185.199.108.153, .109.153, .110.153, .111.153) → 301-redirected to `www.`

GitHub Pages serves from the `/docs` folder on the `main` branch, with HTTPS enforced.
