# Brief: Reframe QC4PDE landing page as a consortium

Edit `index.html` so the site presents QC4PDE as a research consortium, with the
annual workshop as one of its activities. Reuse the existing CSS classes, layout
components, and section styles. Do not introduce new styling unless a component
has no existing equivalent. Leave `events/2026-qce/` content unchanged except for
the footer (see step 8).

## 1. Metadata
- `<title>`: QC4PDE Consortium — Quantum Computing for PDEs
- meta description and og:description: An international research consortium on
  quantum algorithms for partial differential equations.
- og:title: QC4PDE Consortium

## 2. Nav
Mission (#mission) · Activities (#activities) · Events · Committee (#committee) · Join (#join)

## 3. Hero
- Eyebrow: Research Consortium · Est. 2026
- H1: keep "Quantum Computing for Partial Differential Equations"
- Lede: An international consortium connecting quantum-algorithm developers with
  domain scientists to establish where quantum PDE solvers can deliver practical
  utility, and what it will take to get there.
- Primary button: Join the consortium → #join
- Secondary button: QC4PDE 2026 workshop → events/2026-qce/index.html
- Stat strip (replace current three items):
  - Founded: 2026
  - Steering committee: 8 researchers · 6 institutions
  - Next gathering: IEEE QCE 2026 · Toronto, Sept 13

## 4. Mission (replaces "Why this workshop"; id="mission")
- Heading: Why a consortium
- Keep the first two existing paragraphs as they are.
- Replace the third paragraph with:
  Progress so far has come from isolated groups working on different equations,
  encodings, and hardware. The QC4PDE Consortium brings together experts spanning
  **applications, algorithms, software, and hardware** to turn those efforts into
  a shared, measurable research agenda.
- Keep the three focus-area columns (Applications, Algorithms, Software &
  workflows) unchanged.

## 5. Activities (new section; id="activities")
Promote the current "What we're building" paragraph into four cards, using the
same card/column component as the focus areas.
- Heading: What we do
- **Community roadmap.** Identifying the algorithmic, hardware, and software
  milestones required for practical quantum utility in PDE solving.
- **Shared benchmarks.** Defining benchmark problems at engineering-relevant
  scales so groups can compare methods reproducibly.
- **Workshops and gatherings.** An annual workshop at IEEE Quantum Week, plus
  sessions at other venues throughout the year.
- **Collaborations.** Connecting domain-science groups with quantum-algorithm
  developers through joint publications, open-source tools, and proposals.

## 6. Events (keep; shorten)
- Heading: Workshops & gatherings
- Text: The consortium convenes annually at IEEE Quantum Week. Current event:
  QC4PDE @ IEEE QCE 2026, September 13, 2026, Toronto.
- Keep "See all events →" link.

## 7. Steering committee (id="committee")
- Keep all eight names and affiliations as they are.
- Intro: The consortium is guided by a steering committee drawn from national
  laboratories, industry, and academia.

## 8. Join (replaces "Beyond the workshop"; id="join")
- Heading: Join the consortium
- Text: Participation is open to researchers, students, and practitioners working
  on any part of the quantum-PDE stack. Subscribe to the announcement list for
  consortium activities and workshop updates:
  groups.google.com/g/qc4pde-announce. To send to the list, email
  qc4pde-announce@googlegroups.com.
- Keep the "Particularly encouraged..." line.
- Remove all remaining "working group" wording from the page.

## 9. Footers
- Landing footer tagline: Quantum Computing for Partial Differential Equations.
  An international research consortium and workshop series.
- Copyright (both pages): © 2026 QC4PDE Consortium
- Event page footer: rename the "Workshop series" heading to "QC4PDE Consortium",
  and change the "Working group" link to "Join the consortium"
  (../../index.html#join).
- Update footer "Site" links to match the new nav anchors.

## 10. Checks
- Grep the repo for "working group" and "Workshop Organizers" and resolve any
  remaining instances.
- Confirm all in-page anchors resolve.
- Update CLAUDE.md so the Project section describes QC4PDE as a consortium.
