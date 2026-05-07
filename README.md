# QC4PDE Workshop Website

Source for the QC4PDE workshop series website, hosted on GitHub Pages.

**Live site:** https://qc4pde.github.io

---

## What this is

A static, plain-HTML/CSS site — no build step, no framework, no dependencies. Anyone with a text editor can edit any page. The structure is designed to host the **persistent workshop series** (root) plus **individual events** (`events/2026-qce/`, `events/2026-sc/`, `events/2027-qce/`, …) so each event gets a permanent archived URL and the series can host multiple events per year at different conferences.

```
qc4pde.github.io/
├── index.html              ← Persistent home (about, organizers, community)
├── events/
│   ├── index.html          ← Lists all past, current, and upcoming events
│   └── 2026-qce/
│       └── index.html      ← QC4PDE @ IEEE QCE 2026 (Toronto)
├── 2026/
│   └── index.html          ← Redirect to events/2026-qce/ (preserves old links)
├── assets/
│   ├── css/style.css       ← Shared stylesheet for all pages
│   └── img/
│       └── people/         ← Organizer headshots
└── README.md
```

### Naming conventions

Event folders use the format `YYYY-venue` (lowercase): `2026-qce`, `2026-sc`, `2027-qce`. Lowercase URLs avoid case-sensitivity bugs on Linux servers (which is what GitHub Pages runs on) and match standard web conventions. The displayed name on the page can still be styled "QCE 2026" — that's a separate concern from the URL slug.

---

## One-time setup (deployment)

Already complete for the current site. For reference / disaster recovery:

1. **GitHub organization** is `qc4pde`. The repo is `qc4pde.github.io`. Repo name must match the org name + `.github.io` for GitHub to publish at the bare org URL.

2. **Push to `main`** — GitHub Pages serves from `main` / root, configured under *Settings → Pages*.

3. **(Optional) Custom domain**: if `qc4pde.org` is acquired, add a `CNAME` file at the repo root containing just `qc4pde.org`, set DNS A records as instructed by GitHub, and enable HTTPS in Pages settings.

4. **Collaborators**: each co-organizer should have write access via *Settings → Collaborators and teams*. Push via PR or directly to `main`.

---

## How to edit

Every page is a single HTML file. Open it in any editor. The CSS lives in `assets/css/style.css` and is shared across all pages.

### Common edits during the run-up to a workshop

- **EasyChair link (when CFP opens)**: in the relevant event page (e.g., `events/2026-qce/index.html`), find `id="easychair-link"` and replace `href="#"` with the actual EasyChair URL.
- **Confirming speakers**: in the speakers section, mark confirmed vs invited.
- **Program details**: replace placeholder talk titles in the program section as they firm up.
- **Accepted papers (post-acceptance)**: add a new section after the program section with the list and links to preprints.
- **Slides & recordings (post-workshop)**: add links inline within the program section.

### Editing relative paths — important

Pages live at different depths in the directory tree, which affects how relative paths in `<link>`, `<img>`, and `<a href>` tags work.

| Page location | CSS path | Asset path | Link to home |
|---|---|---|---|
| `/index.html` (root) | `assets/css/style.css` | `assets/img/...` | `index.html` |
| `/events/index.html` | `../assets/css/style.css` | `../assets/img/...` | `../index.html` |
| `/events/2026-qce/index.html` | `../../assets/css/style.css` | `../../assets/img/...` | `../../index.html` |

When copying a page to a new location, remember to adjust the `../` count.

### Local preview

To preview the site locally before pushing:

```bash
cd qc4pde.github.io
python3 -m http.server 8000
# then visit http://localhost:8000
```

This serves the site exactly as GitHub Pages would. Don't preview by double-clicking `index.html` — `file://` URLs handle relative paths differently and will mislead you.

---

## Adding a new event

When QC4PDE is hosted at a new conference, here's the workflow:

1. **Copy an existing event folder as a template:**
   ```bash
   cp -r events/2026-qce events/2027-qce
   ```

2. **Edit `events/2027-qce/index.html`** — update dates, venue, deadlines, speakers, program, and any conference-specific links (registration, submission portal, etc.).

3. **Update `events/index.html`** to add a new entry for the event:
   - Add a new `<div class="edition">` block under the appropriate year section.
   - When a previous event becomes past, change its status class from `live` to `archived`.
   - Add a new year section (`<section><span class="eyebrow">2027</span>...`) when needed.

4. **Update `index.html`** (the persistent home) — update the "Current event" callout in the Events section to point to the new event.

5. **Leave existing event folders untouched** — they become permanent archives at their original URLs. Past events retain `qc4pde.github.io/events/2026-qce/` forever.

6. **Commit and push.** Done.

---

## Yearly rollover

When transitioning to a new year (e.g., end of 2026 → 2027 announcements):

- Mark passed events as `archived` in `events/index.html`.
- Update the home page's "Current event" callout to point to whatever's coming up next.
- The Important Dates table on past event pages can be left as-is — those dates are historical record now.

---

## Adding organizer photos

Drop square JPEGs into `assets/img/people/` named by lowercase first name or last name (e.g., `murali.jpg`, `pooja.jpg`). The `.person .photo` CSS rule handles sizing — see `assets/css/style.css`.

If a photo isn't available for someone yet, just leave the `<img>` tag out for that person — the layout handles missing photos gracefully.

---

## Design notes

- **Fonts**: Fraunces (serif headings), Inter (body), JetBrains Mono (labels, dates, code). Loaded from Google Fonts CDN.
- **Color tokens** are CSS variables defined at the top of `style.css`. Change there to retheme everything.
- **No JavaScript** is required for the site to function. The hero animation is CSS-only and respects `prefers-reduced-motion`.
- **Mobile responsive** via standard CSS grid + media queries.
- **Accessibility**: semantic HTML, sufficient color contrast, focus styles inherited from browser defaults. Add descriptive `alt` text to any photos uploaded to `assets/img/`.

---

## Things to add later (optional)

- **Accepted papers page** post-notification: add `events/2026-qce/papers.html` with the list, link from the event page.
- **Post-workshop summary**: add `events/2026-qce/summary.html` with key discussions, working group outcomes, links to slides/recordings.
- **Mailing list embed**: if a Google Group or other list is set up, embed or link the signup form in the Community section of `index.html`.
- **Favicon**: drop `favicon.ico` (or `.svg`) at the root and add `<link rel="icon" href="/favicon.ico">` to the `<head>` of each page.
- **Sponsor logos**: if relevant, add a sponsors section before the footer.
- **Resources page**: a top-level `resources/` folder for benchmark repos, roadmap drafts, talks/slides archive — scales the same way as `events/`.
- **Analytics**: if traffic stats are wanted, [GoatCounter](https://www.goatcounter.com/) or [Plausible](https://plausible.io/) are privacy-friendly options that won't trigger institutional concerns the way Google Analytics might at a national lab.

---

## URL stability

Once a URL is published (in a workshop proposal, paper, email, social media), it should keep working forever. The site uses redirect stubs (e.g., `/2026/index.html`) to preserve old URLs after restructuring. If you reorganize folders in the future, follow the same pattern: leave a tiny HTML file at the old location with a `<meta http-equiv="refresh">` pointing to the new location.

---

## Contact

Workshop main contact: Muralikrishnan Gopalakrishnan Meena, gopalakrishm@ornl.gov

Site issues: open an issue at https://github.com/qc4pde/qc4pde.github.io/issues