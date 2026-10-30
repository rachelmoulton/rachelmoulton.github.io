<!--
Maintainer notes (stripped from Claude's context):
- Created 2026-10-30. Folder + assets only; no pages built yet.
- headshot.png copied from a chat-pasted image (1091x1442, ~3.2 MB PNG) — not yet optimized.
- resume.pdf copied from ~/Desktop/MBA/RachelMoulton_Resume_2026.pdf (the .docx source lives beside it).
-->

# Personal Site — Rachel Moulton

## What this is

- Rachel's personal resume + portfolio website.
- Audience: recruiters/employers and her BYU MBA network.
- Rachel: BYU MBA (Marketing track, 2025–2027); Chief of Staff, AI Foundry @ BYU.
- Positioning line: "Project Management & Analytics · Applied AI Architecture · Competitive Strategy".

## Tech

- Plain HTML + CSS. Minimal vanilla JavaScript only when a feature truly needs it.
- No framework, no build step, no package manager, nothing to install.
- Must be responsive (works on phones) and print cleanly (add a `@media print` stylesheet for the resume page).
- 3D: Google's `<model-viewer>` web component loaded from a CDN with an exact pinned version
  (e.g. `@google/model-viewer@<exact version>`, never `@latest`). Use three.js only if model-viewer can't do what's needed.

## Preview

- Simplest: double-click `index.html` to open it in a browser.
- If the 3D page doesn't load models from a `file://` URL, run a local server from this folder:
  `python3 -m http.server 8000` then open http://localhost:8000.

## Hosting

- Vercel, as a static site (no config file needed).
- Deploying, logging in, or changing domains touches the public internet — **always confirm with Rachel first.**

## Layout

```
personal-site/
├── CLAUDE.md
├── index.html          # Resume (home) — not built yet
├── interactive.html    # 3D / interactive page — not built yet
├── portfolio.html      # Portfolio tab — not built yet
├── styles.css          # shared styles — not built yet
└── assets/
    ├── headshot.png    # Rachel's headshot (needs resizing before launch)
    ├── resume.pdf      # source of truth for resume content
    ├── portfolio/      # images/PDFs for portfolio entries
    └── 3d/             # .glb files exported from Blender
```

## Pages

All pages share one top nav: **Resume · Interactive · Portfolio**.

### 1. Resume — `index.html` (home)

One page whose layout mirrors her actual resume (assets/resume.pdf):
- Name + contact block at top; headshot visible.
- Centered headline "Project Management & Analytics", subtitle
  "Applied AI Architecture • Competitive Strategy • BYU MBA".
- Ruled sections in this order: **Education, Experience, Volunteer, Personal.**
- Section headings in ALL CAPS with a horizontal rule under them.
- Each entry: employer/school | location on the left, dates right-aligned; role in italics; then bullets.
- A "Download PDF" link to `assets/resume.pdf`.

### 2. Interactive — `interactive.html`

- Shows interactive 3D graphics Rachel builds in Blender; reachable with one click from the resume.
- Workflow: in Blender, File → Export → glTF 2.0, format **.glb** → save into `assets/3d/` → add a `<model-viewer>` tag pointing at it.
- Keep each .glb under ~10 MB (decimate meshes, compress textures) so pages load fast.

### 3. Portfolio — `portfolio.html`

- Static site: "uploading" = drop a file into `assets/portfolio/`, add an entry, redeploy.
  No live upload form (that needs a database + login — out of scope unless Rachel asks).
- Every entry has the same fields: **title, 1–2 sentence description, Rachel's role, and an image / PDF / link.**
- Keep entries in one clearly marked, copy-paste-friendly block so adding a new one is just duplicating it.
- Candidate items (Rachel must confirm each is OK to show publicly before it goes live):
  AI Foundry tools, case competitions, Weber State data analytics portfolio, I Love You Bro annual report.

## Always / never

- **Always** treat `assets/resume.pdf` as the source of truth for resume content; keep site text in sync with it.
  Never invent accomplishments, titles, or numbers.
- **Never** publish Rachel's phone number on the site by default (public sites get scraped). Email + LinkedIn only, unless she says otherwise.
- **Always** keep the design original — don't copy colors or layouts from other people's portfolio templates.
  Mirroring her own resume's layout is fine.
- **Never** add frameworks, trackers, analytics, or third-party scripts without asking (model-viewer is the approved exception).
- **Always** optimize images before they ship: resize the headshot (e.g. ~600 px wide JPEG) and large portfolio images with
  macOS `sips`, e.g. `sips -Z 800 -s format jpeg in.png --out out.jpg`. Keep originals out of the deployed folder if they're huge.
- **Always** add `alt` text to images and a descriptive `alt` to each `<model-viewer>`.

## Open questions (ask Rachel)

- Phone number on the site: yes or no? (Default: no.)
- Which portfolio items are OK to make public?
- Custom domain, or the default `*.vercel.app` URL?
- Color and font preferences?
