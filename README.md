# QC4PDE Consortium Website

Source for the QC4PDE (Quantum Computing for Partial Differential Equations)
Consortium website, hosted on GitHub Pages.

**Live site:** https://qc4pde.github.io

Anyone can suggest changes with a pull request. To be added to the
[qc4pde GitHub organization](https://github.com/qc4pde), send your GitHub
username to the Steering & Outreach co-chairs.

---

## How the site is built

The site mixes two kinds of pages:

- **HTML pages** (the landing page and events) are hand-written and use
  `assets/css/style.css` directly.
- **Markdown pages** (charter, committees, meetings) are turned into HTML by
  GitHub Pages' built-in Jekyll when you push to `main`, using the shared
  layout in `_layouts/default.html` (header, nav, footer, styles).

There is no build step to run yourself. Push to `main` and GitHub Pages
publishes the site within a minute or two.

```
qc4pde.github.io/
├── index.html                  ← Landing page (mission, committees, events, members, join)
├── charter/
│   ├── index.md                ← Full charter
│   └── summary.md              ← Executive summary
├── committees/
│   ├── index.md                ← Committees overview
│   ├── steering/index.md       ← Steering & Outreach (+ dated update docs)
│   ├── benchmarks/index.md     ← Benchmarks & Stewardship
│   └── software/index.md       ← Software & Tooling (+ assets.md)
├── meetings/
│   ├── index.md                ← Schedule and table of agendas/minutes
│   ├── YYYY-MM-DD-agenda.md
│   ├── YYYY-MM-DD-minutes.md
│   ├── join.html               ← Zoom link behind an hCaptcha check
│   └── assets/                 ← Meeting images (transcripts are git-ignored)
├── events/
│   ├── index.html              ← All workshops and community events
│   └── 2026-qce/index.html     ← QC4PDE @ IEEE QCE 2026 (Toronto)
├── _layouts/default.html       ← Layout for all Markdown pages
└── assets/
    ├── css/style.css           ← Shared stylesheet
    └── img/people/             ← Headshots
```

### Rules for Markdown pages

- **Name a folder's main page `index.md`, not `README.md`.** GitHub Pages
  publishes `README.md` as `README.html`, so `committees/steering/` would
  return "not found".
- **Start each page with a title** so the browser tab is named:
  ```markdown
  ---
  title: "Meeting · 2026-12-11 · Agenda"
  ---
  ```
- **Inside Markdown, link to the `.md` file**
  (e.g. `[agenda](2026-12-11-agenda.md)`). GitHub Pages rewrites these to
  `.html`.
- **Inside HTML pages, link to the published address**, not the `.md` file:
  `charter/`, `charter/summary.html`, `meetings/`.
- **The nav is written out in four places.** Keep `index.html`,
  `events/index.html`, `events/2026-qce/index.html` (its footer), and
  `_layouts/default.html` in sync when it changes.

---

## Common tasks

### Before a meeting

1. Copy the previous agenda and minutes to `meetings/YYYY-MM-DD-agenda.md`
   and `meetings/YYYY-MM-DD-minutes.md`, and update the dates and titles.
2. Add a row at the top of the table in `meetings/index.md`.
3. Open a GitHub issue titled "YYYY-MM-DD Meeting — agenda input" so
   members can add or flag items. The chair updates the agenda by the
   morning of the meeting.

### After a meeting

1. Save the Zoom transcript in `meetings/assets/meeting-transcripts/`. This
   folder is git-ignored, so transcripts stay local.
2. Combine live notes with an LLM summary of the transcript in the minutes
   file, including the action-items table (Item · Owner · Due ·
   Status / Notes).
3. Set up the next meeting's agenda and minutes files.

### Committee updates

Each committee page has a **Status** section linking to dated update docs
(e.g. `committees/steering/updates_2026-11-20.md`). Add a new dated doc for
each update and link it from both the committee page and that meeting's
agenda.

### Changing the Zoom link

`meetings/join.html` stores the meeting details as base64-encoded HTML in
`MEETING_INFO`, so the URL and passcode aren't in the page as plain text. To
change them, encode the new HTML block and replace the string:

```bash
python3 -c 'import base64,sys; print(base64.b64encode(sys.stdin.read().encode()).decode())' <<'EOF'
<p><a href="https://...">Join Zoom Meeting</a></p><p>Meeting ID: ...<br>Passcode: ...</p>
EOF
```

The hCaptcha sitekey in that page is public and safe to commit. **Never
commit the hCaptcha secret.** The check only deters crawlers and casual
scraping: it runs in the browser, and the encoded details can still be
decoded from the page source by anyone determined.

### Adding an event

1. Copy an existing event folder: `cp -r events/2026-qce events/2027-qce`.
2. Edit the new page's dates, venue, deadlines, speakers, and program.
3. Add an entry to `events/index.html`. Mark past events `archived` instead
   of `live`.
4. Update the "Current event" callout and the hero's "Next gathering" on
   `index.html`.
5. Leave past event folders as they are; they are permanent archives.

Event folders use lowercase `YYYY-venue` names (`2026-qce`, `2027-qce`) to
avoid case-sensitivity problems on GitHub Pages.

### Relative paths in HTML pages

| Page location | CSS path | Asset path | Link to home |
|---|---|---|---|
| `/index.html` | `assets/css/style.css` | `assets/img/...` | `index.html` |
| `/events/index.html` | `../assets/css/style.css` | `../assets/img/...` | `../index.html` |
| `/events/2026-qce/index.html` | `../../assets/css/style.css` | `../../assets/img/...` | `../../index.html` |

Markdown pages don't need this: the layout uses site-relative paths.

### Member photos

Drop square JPEGs into `assets/img/people/` (e.g. `murali.jpg`). The
`.person .photo` CSS rule handles sizing; leave out the `<img>` tag for
anyone without a photo.

---

## Previewing changes

- **HTML pages:** `python3 -m http.server 8000`, then open
  http://localhost:8000. Don't double-click files: `file://` links behave
  differently.
- **Markdown pages:** the simple server shows them as raw text, because only
  Jekyll renders them. Either check the live site after merging, or run
  Jekyll locally with the GitHub Pages gem. This needs a newer Ruby than
  macOS's built-in 2.6 (e.g. `brew install ruby`):
  ```bash
  printf 'source "https://rubygems.org"\ngem "github-pages", group: :jekyll_plugins\n' > Gemfile
  bundle install && bundle exec jekyll serve
  # then visit http://localhost:4000
  ```

---

## Design notes

- **Fonts:** Fraunces (headings), Inter (body), JetBrains Mono (labels,
  dates). Loaded from Google Fonts.
- **Colors** are CSS variables at the top of `style.css`; change them there
  to retheme everything.
- **JavaScript** is used only on `meetings/join.html` (the CAPTCHA). The
  hero animation is CSS-only and respects `prefers-reduced-motion`.
- **Responsive** via CSS grid and media queries.
- **Accessibility:** semantic HTML, sufficient contrast, and descriptive
  `alt` text on images.

---

## URL stability

Once a URL is published (in a proposal, paper, or email), it should keep
working. If you move a page, leave a small HTML file at the old location
with `<meta http-equiv="refresh" content="0; url=NEW-URL">`.

---

## Deployment

- The GitHub organization is `qc4pde`, and the repo is `qc4pde.github.io`,
  which publishes at the bare org URL.
- GitHub Pages serves `main` from the repo root (*Settings → Pages*).
- **Custom domain (optional):** add a `CNAME` file containing the domain, set
  the DNS records GitHub lists, and enable HTTPS in Pages settings.

---

## Contact

Main contact: Muralikrishnan Gopalakrishnan Meena, gopalakrishm@ornl.gov

Site issues: https://github.com/qc4pde/qc4pde.github.io/issues
