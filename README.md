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

The page fetches `https://laurenlev10.github.io/lauren-agent-hub-data/state/subscribe_target.json` on load and uses:
- `form_id` → the SimpleTexting webForm for the upcoming event's contact list
- `ig_reel_url` / `fb_url` / `tiktok_url` → per-event share buttons
- `city`/`state`/`start_date`/`end_date` → "Next event" pill

That JSON is updated daily at 06:00 PT by the `update-subscribe-target.yml` workflow in `lauren-agent-hub-data`. If the fetch fails, the form falls back to the most-recent known good `form_id`.

## Custom domain

DNS is configured at GoDaddy:
- `www.themakeupblowoutsale-group.com` → CNAME → `laurenlev10.github.io`
- `themakeupblowoutsale-group.com` (apex) → 4× A records to GitHub Pages IPs (185.199.108.153, .109.153, .110.153, .111.153) → 301-redirected to `www.`

GitHub Pages serves from the `/docs` folder on the `main` branch, with HTTPS enforced.
