# Watershed Hydrology Lab — Website

Public-facing website for the **Watershed Hydrology Lab** at the
University of Florida / IFAS Range Cattle Research and Education
Center (RCREC), led by Dr. Golmar Golmohammadi.

- **Live URL:** [https://watershedhydrologylab.com](https://watershedhydrologylab.com)
- **Repository:** [github.com/waterhydrolab](https://github.com/waterhydrolab)
- **Theme:** [al-folio](https://github.com/alshedivat/al-folio) — a Jekyll
  theme designed for academic groups.
- **Hosting:** Cloudflare Pages (build runs on Cloudflare on every
  push to `main`). See [`DEPLOY.md`](./DEPLOY.md) for the full pipeline.
  GitHub Actions runs a parallel build as a CI safety-net only.

This README explains what each part of the repository does and how to
make common changes. **It is meant to be readable by someone who has
never used Jekyll or GitHub before** — please skim it before editing
anything.

If you only want to know "how do I update X?", jump straight to
[Common edits](#common-edits).

---

## 1. Repository layout

```
.
├── _config.yml                ← Master site configuration (heavily commented).
├── CNAME                      ← Custom domain (watershedhydrologylab.com).
│
├── _pages/                    ← Top-level pages (one Markdown file = one page).
│   ├── about.md                  ← Homepage (/)
│   ├── profiles.md               ← People page (/people/)
│   ├── about_<name>.md           ← Bio content for each lab member
│   ├── projects.md               ← Research index (/projects/)
│   ├── publications.md           ← Publications list (/publications/)
│   ├── facilities.md             ← Field & lab equipment (/facilities/)
│   ├── news.md                   ← News archive (/news/)
│   └── cv.md                     ← (Hidden — turn on in front matter when ready)
│
├── _projects/                 ← One file per research theme. Cards on /projects/.
│   ├── 1_hydrologic_modeling.md
│   ├── 2_ai_risk_mapping.md
│   └── 3_decision_support.md
│
├── _news/                     ← One file per news item. Most recent appears on homepage.
│
├── _bibliography/
│   └── papers.bib             ← Publications in BibTeX. Edit to add/remove papers.
│
├── _data/
│   └── socials.yml            ← Social/profile links (X, LinkedIn, ORCID, Scholar, …)
│
├── assets/
│   ├── img/team/              ← Profile photos (one per member)
│   ├── img/publications/      ← Publication thumbnails
│   ├── img/research_*         ← Research-card images (placeholders for now)
│   └── pdf/                   ← PDFs (CV, reports) you want to link to
│
├── .github/workflows/
│   └── deploy.yml             ← GitHub Actions: builds and deploys on every push
│
├── Gemfile, Gemfile.lock      ← Ruby dependencies for local development
├── package.json               ← Node dependencies (used by build for purgecss/Tailwind)
└── docs/                      ← al-folio's own documentation (kept for reference)
```

Anything outside this list is part of the al-folio theme machinery —
you generally don't need to touch it.

---

## 2. Common edits

### Add a new lab member

1. Drop their photo in `assets/img/team/<firstname>_<lastname>.jpg`
   (square, ~400 × 400 px).
2. Create a bio file `_pages/about_<firstname>.md` — copy one of the
   existing files as a template.
3. Open `_pages/profiles.md` and add a new block to the `profiles:`
   list. Alternate `align: left` and `align: right` as you go.
4. Commit and push. The site will rebuild automatically.

### Add a new publication

1. Open `_bibliography/papers.bib`.
2. Paste the BibTeX entry from the publisher. Use a unique citekey such
   as `lastnameYEARkeyword`. The PI's name (`Golmohammadi`) is
   automatically bolded in citations.
3. Optionally add a thumbnail to `assets/img/publications/` and link it
   with `preview = {publications/yourfile.jpg}` in the BibTeX entry.
4. Mark a paper as featured on the homepage with `selected = {true}`.

### Post a news item

1. Create `_news/announcement_<NUM>_<slug>.md`. Use the existing files
   as templates. Front matter:
   ```yaml
   ---
   layout: post
   date: 2026-05-27 12:00:00-0400
   inline: true # set false if it needs its own full page
   related_posts: false
   ---
   ```
2. Below the second `---`, write the announcement in Markdown.

### Add or rename a top-nav link

1. Open the page in `_pages/`. In the YAML front matter, set
   `nav: true` and choose a `nav_order` (lower = leftmost in the menu).
2. The `title:` field controls the menu label.

### Update social-media or academic-profile links

Edit `_data/socials.yml`. Every key is explained inline.

### Change the lab description on the homepage

Open `_pages/about.md` and edit the Markdown below the front matter.

### Change the domain

1. Edit `_config.yml` — update the `url:` field.
2. Replace the contents of `CNAME` with the new domain.
3. Update DNS records at your registrar (see `SETUP.md` § 4).

---

## 3. Building the site locally (optional)

You only need this if you want to preview changes before pushing. If
you push to GitHub, the live site is rebuilt automatically.

### Requirements

- Ruby 3.3.x and Bundler
- Node 20.x
- ImageMagick (`brew install imagemagick` on macOS)

### One-time setup

```bash
bundle install
npm install
```

### Run the dev server

```bash
bundle exec jekyll serve --livereload
```

Open <http://localhost:4000> in your browser. Edits to Markdown files
are picked up automatically; changes to `_config.yml` require a server
restart.

If you don't want to install Ruby/Node directly, the repo includes a
`Dockerfile` and `docker-compose.yml`. Run `docker compose up` and the
site will be served at <http://localhost:8080>.

---

## 4. Deployment (how the site goes live)

Every push to the `main` branch triggers a **Cloudflare Pages** build,
which:

1. Installs Ruby, Node, Python, and ImageMagick on a clean Cloudflare
   build container (versions pinned in `.tool-versions` and in the
   Pages project environment variables).
2. Runs `bundle exec jekyll build` to generate the static site into
   `_site/`.
3. Purges unused CSS to keep the bundle small.
4. Publishes `_site/` to Cloudflare's CDN, fronted by the domain
   [watershedhydrologylab.com](https://watershedhydrologylab.com).

Pull requests get their own preview URL automatically.

The companion workflow [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)
runs the same build on GitHub Actions as a CI safety-net (no deploy
step). If the build breaks there, the PR is blocked before Cloudflare
even tries.

See [`DEPLOY.md`](./DEPLOY.md) for the one-time wire-up between this
repo and Cloudflare Pages (build settings, env vars, DNS delegation).
[`SETUP.md`](./SETUP.md) describes the older GitHub-Pages-only flow and
is kept for historical reference.

---

## 5. Things to confirm before going live

The following items were drawn from public sources or carried over from
the old site. Please verify each one before the launch:

- [ ] **Google Scholar profile ID** in `_data/socials.yml`
      (`scholar_userid: cpXxmlYAAAAJ`). I picked the most-likely match;
      please confirm.
- [ ] **Lab email** in `_data/socials.yml`. Default is
      `g.golmohammadi@ufl.edu`. The old site used a separate Gmail
      (`hydrologyrcrecflorida@gmail.com`) — decide which to use.
- [ ] **Phone number on the homepage** (`_pages/about.md`). The current
      value `(863) 374-7053` is from the SWES faculty page. The old site
      showed a placeholder (`1-800-555-5555`).
- [ ] **Team photos.** The supervisor's official UF/IFAS photo is
      included; everyone else has a placeholder SVG with their initials.
      Replace each `assets/img/team/<name>.svg` with a real JPG/PNG when
      available.
- [ ] **Research images.** The three project cards use placeholder SVGs
      (`assets/img/research_placeholder_*.svg`). Replace with real photos
      from the field or with diagrams.

---

## 6. Credit and licensing

This site is built on top of the [al-folio](https://github.com/alshedivat/al-folio)
Jekyll theme, distributed under the MIT license. The theme's copyright
and license are preserved in `LICENSE`.

Site content (text, photos, lab branding) is © Watershed Hydrology Lab
unless otherwise noted.
