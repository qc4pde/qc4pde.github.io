# QC4PDE Workshop Website

Source for the QC4PDE workshop series website, hosted on GitHub Pages.

**Live site:** https://qc4pde.github.io

---

## What this is

A static, plain-HTML/CSS site — no build step, no framework, no dependencies. Anyone with a text editor can edit any page. The structure is designed to host the **persistent workshop series** (root) plus **per-year editions** (`2026/`, `2027/`, ...) so each annual edition gets a permanent archived URL.

```
qc4pde.github.io/
├── index.html              ← Persistent home (about, organizers, all editions)
├── 2026/
│   └── index.html          ← QC4PDE 2026 @ IEEE QCE 2026
├── assets/
│   ├── css/style.css       ← Shared stylesheet for all pages
│   └── img/                ← Photos, logos
└── README.md               ← This file
```

---

## One-time setup (deployment)

1. **Create a GitHub organization** named `qc4pde` (any organizer can do this; one of you should be the owner, with at least one other co-owner for redundancy).

2. **Create a repository** in that org named exactly `qc4pde.github.io`. The repo name must match the org name + `.github.io` for GitHub to publish it at the bare org URL.

3. **Push this directory** to that repo:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin git@github.com:qc4pde/qc4pde.github.io.git
   git push -u origin main
   ```

4. **Enable GitHub Pages**: in the repo, go to *Settings → Pages*. Under "Build and deployment", set Source to "Deploy from a branch", branch to `main`, folder to `/ (root)`. Save. The site will be live at `https://qc4pde.github.io` within ~1 minute.

5. **(Optional) Custom domain**: if you buy `qc4pde.org` (~$12/yr at any registrar), add a `CNAME` file at the repo root containing just `qc4pde.org`, set the DNS A records as instructed by GitHub, and enable HTTPS in Pages settings.

6. **Add organizer collaborators**: in *Settings → Collaborators and teams*, give each co-organizer write access. Each pushes via PR or directly to `main`.

---

## How to edit

Every page is a single HTML file. Open it in any editor. The CSS is in `assets/css/style.css` and is shared across all pages.

**To update the 2026 edition** (speakers confirming, EasyChair link going live, program details firming up): edit `2026/index.html` and push.

The most common edits during the run-up to the workshop:

- **EasyChair link (when CFP opens):** in `2026/index.html`, find `id="easychair-link"` and replace `href="#"` with the actual EasyChair URL.
- **Confirming speakers:** in the speakers section, you can add a class or rearrange to mark confirmed vs invited.
- **Program details:** as titles and orderings firm up, replace placeholder talk titles in the program section.
- **Adding accepted papers (post-acceptance):** add a new section after the program section with the list.
- **Post-workshop slides/recordings:** add links inline within the program section.

---

## Yearly rollover (creating QC4PDE 2027 next year)

When QCE 2027 is announced, here's the process:

1. **Copy the current edition folder:**
   ```bash
   cp -r 2026 2027
   ```

2. **Edit `2027/index.html`** to update dates, venue, deadlines, and content for the new edition. Keep the same structure.

3. **Update `index.html`** (the root):
   - Add a new entry in the `<div class="editions">` block for 2027 with status `live`
   - Change the 2026 entry's status from `live` to `archived` (CSS class `archived` is already styled)
   - Update the "Current edition" hero metadata and the footer "Current edition" links to point to 2027
   - Update the main CTA in the hero from `2026/index.html` to `2027/index.html`

4. **Leave `2026/` untouched** — it becomes the permanent archive. Past editions retain their URL forever (`qc4pde.github.io/2026/`).

5. **Commit and push.** Done.

---

## Design notes

- **Fonts:** Fraunces (serif headings, gives editorial-academic gravitas), Inter (body), JetBrains Mono (labels, dates, code). Loaded from Google Fonts CDN.
- **Color tokens** are CSS variables defined at the top of `style.css`. Change there to retheme everything.
- **No JavaScript** is required for the site to function. The hero animation is CSS-only and respects `prefers-reduced-motion`.
- **Mobile responsive** via standard CSS grid + media queries.
- **Accessibility:** semantic HTML, sufficient color contrast, focus styles inherited from browser defaults. Add `alt` text to any photos you upload to `assets/img/`.

---

## Things to add later (optional)

- **Organizer photos:** drop `.jpg`s into `assets/img/people/`, then add `<img>` to each `.person` block. The CSS doesn't currently style photos — easy to add when needed.
- **Accepted papers page** post-notification: add `2026/papers.html` with the list, link from main page.
- **Post-workshop summary**: add `2026/summary.html` with key discussions, working group outcomes, links to slides/recordings.
- **Mailing list embed:** if you set up a Google Group or Mailchimp list, embed the signup form in the Community section of `index.html`.
- **Favicon:** drop `favicon.ico` (or `.svg`) at the root and add `<link rel="icon" href="/favicon.ico">` to the `<head>` of each page.
- **Sponsor logos:** if relevant, add a sponsors section before the footer.
- **Analytics:** if you want traffic stats, [GoatCounter](https://www.goatcounter.com/) or [Plausible](https://plausible.io/) are privacy-friendly options that won't trigger IRB or institutional concerns the way Google Analytics might at a national lab.

---

## Contact

Workshop main contact: Muralikrishnan Gopalakrishnan Meena, gopalakrishm@ornl.gov

Site issues: open an issue at https://github.com/qc4pde/qc4pde.github.io/issues
