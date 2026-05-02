# Improvements Roadmap

Tracking suggested improvements for the Mac Admin Conferences Calendar. Grouped by theme; check off as completed.

## 1. Home page scaling

As the upcoming list fills out, the flat 10-item list becomes awkward.

- [x] Group upcoming events by year, then by month, with month headers (e.g. `June 2026`, `July 2026`)
- [x] Show full cards for the next ~3 months, then collapse the rest into a compact one-line-per-event summary (`Sept 30 · MacSysAdmin · Göteborg`)
- [x] Add a "View all upcoming →" link at the end of the compact tail
- [x] Cap "Recent Events" at 3–5; let the events page handle history
- [ ] Add an "ICS subscribe" / "Add to calendar" button near the top (see §7)

## 2. Dark mode

No dark mode today; colors are baked into `static/css/style.css` and inlined in `calendar/list.html`.

- [ ] Move all colors to CSS custom properties on `:root` and `:root[data-theme="dark"]`
- [ ] Default to `prefers-color-scheme`, with a header toggle that persists in `localStorage`
- [ ] Inline a pre-paint script in `<head>` that sets `data-theme` before first render to avoid FOUC
- [ ] Expose both light and dark accent colors via `params` in `hugo.toml`
- [ ] Delete unused `assets/css/main.css`
- [ ] Move the `<style>` block at the bottom of `calendar/list.html` into the main stylesheet
- [ ] Consolidate `dynamic-css.html` partial into the main stylesheet (use CSS variables only)

## 3. Accessibility pass

- [ ] Add textual "Past" / "Upcoming" labels to status badges (don't rely on color alone)
- [ ] Fix contrast on `.calendar-event.multi-day` (#28a745 + white is ~3:1, fails AA for small text)
- [ ] Bump mobile calendar event font above 0.6rem, or hide labels on small screens
- [ ] Replace `opacity: 0.7` on past events with a dedicated muted color token
- [ ] Add `rel="noopener noreferrer"` to all `target="_blank"` links — implement via Hugo render-link hook
- [ ] Wrap emoji icons in `<span aria-hidden="true">` so screen readers don't announce "calendar emoji" etc.
- [ ] Convert clickable `<div class="calendar-event">` pills to `<button>` or `<a>` for keyboard + screen reader support
- [ ] Move focus to the event details panel after click (set `tabindex="-1"`, call `.focus()`)
- [ ] Add a skip link: `<a class="skip-link" href="#main">Skip to content</a>` + `<main id="main">`
- [ ] Fix heading order — site title in nav should not be `<h1>` if the page also has an `<h1>`
- [ ] Remove the wrapping `<p>{{ .Content }}</p>` in `events/list.html` and `calendar/list.html` (Hugo already renders `<p>` from markdown — invalid nested HTML)
- [ ] Remove deprecated `canonifyURLs = true` from `hugo.toml`
- [ ] Add `aria-label="Previous month"` / `aria-label="Next month"` to calendar nav buttons

## 4. Multi-day events spanning cells

Today each day a multi-day event covers gets its own separate pill. The CSS has an unused `.calendar-event.multi-day` class.

- [ ] Render the calendar as 7-column grid weeks with absolutely-positioned event bars spanning day columns
- [ ] Split events that cross a week boundary into two bars (Sat-end + Sun-start)
- [ ] Compute "event lanes" per week so overlapping events stack vertically without colliding
- [ ] Keep per-day pill rendering as the mobile fallback below ~600px
- [ ] Wire up the existing `.calendar-event.multi-day` CSS class

## 5. Visual polish: backgrounds / logos

- [ ] Add an optional `logo` or `image` field to event schema in `events.yaml`
- [ ] Use Hugo image processing to produce thumbnails + LQIP
- [ ] Cards: render small logo as left-side avatar, OR faint full-card background (~5–8% opacity)
- [ ] Provide a fallback: type-based subtle pattern or icon (conference / meetup / workshop / webinar)
- [ ] Verify card text contrast remains AA-compliant with backgrounds applied

## 6. Events page improvements

- [ ] Default sort: upcoming-first ascending, then past descending (currently `sort "desc"` mixes years)
- [ ] Replace JS filter with server-rendered `#upcoming` / `#past` sections (works without JS)
- [ ] Layer JS-progressive filtering on top for type / region / language
- [ ] Group past events by year using collapsible `<details>` per year
- [ ] Add a client-side search box (fuzzy match on name/location)

## 7. Static-site features

- [ ] Generate `events.ics` at build time via a Hugo output format ("subscribe to calendar" — biggest community win)
- [ ] Generate `events.json` feed for downstream consumers
- [ ] Add JSON-LD `Event` structured data per card for Google search results
- [ ] Add Open Graph / Twitter card meta tags in `<head>`
- [ ] Add an RSS feed for newly added events
- [ ] Verify Hugo sitemap is enabled
- [ ] Add a CI step that validates `events.yaml`: required fields, well-formed dates, `end_date >= start_date`

## 8. Code health

- [ ] Extract inline calendar JS to `assets/js/calendar.js` (fingerprinted + minified by Hugo)
- [ ] Pass event data via `<script type="application/json" id="events-data">` instead of string-interpolating into JS literals (current approach breaks on quotes in event names)
- [ ] Remove unused `assets/css/main.css`

---

## Suggested sequencing

1. **Quick wins:** §3 a11y fixes, §8 CSS/JS cleanup, §7 ICS + JSON-LD — ~half day, lowest risk
2. **Dark mode + token consolidation** (§2) — ~half day
3. **Home page restructuring** (§1) — ~1 hour
4. **Events page upgrades** (§6) — ~half day
5. **Multi-day calendar spans** (§4) — ~1 day, mostly JS
6. **Logos / imagery pipeline** (§5) — ~half day plus per-event content work
