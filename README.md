# Watershed Hydrology Lab — Website

Public-facing website for the **Watershed Hydrology Lab** at the University of
Florida / IFAS Range Cattle Research and Education Center (RCREC), led by
Dr. Golmar Golmohammadi.

- **Live site:** <https://watershedhydrologylab.com>
- **Content editor (CMS):** <https://watershedhydrologylab.com/admin/>
- **Repository:** `HugoMachadoRodrigues/waterhydrolab.github.io` (branch `main`)
- **Built with:** [Jekyll](https://jekyllrb.com/) + the
  [al-folio](https://github.com/alshedivat/al-folio) academic theme (v1 "thin
  starter"), a custom earth-tone design system (`assets/whl.css`), and
  [Sveltia CMS](https://github.com/sveltia/sveltia-cms) for browser editing.
- **Hosting:** Cloudflare Pages — every push to `main` rebuilds and publishes
  automatically (~5 min). GitHub Actions runs the same build as a CI safety-net.

---

## 1. Editing the site — two ways

**A. Through the CMS (no code — for non-technical editors).**
Go to **<https://watershedhydrologylab.com/admin/>**, sign in with a GitHub
account that has write access, and fill in forms. Saving commits to `main` and
the site rebuilds itself. The CMS can edit, with click-to-upload images:

- **Home** — hero tagline, the three research pillars, the PI card, intro text.
- **News & Announcements** — add posts with an optional **headline** + **photo**.
- **Research Projects** — title, **cover/banner image**, description, order, body.
- **Team / People** — members (drag to reorder, photo, role, bio) + alumni grid.
- **Other Pages** — **Facilities** (instruments, lab equipment, Field Gallery —
  each a list with photo/video uploads), **Contact** (PI card, map, affiliated
  units, buttons), and the **News** / **Publications** page links.

Full editor guide: **[`CMS-SETUP.md`](./CMS-SETUP.md)** (includes how to grant
access and how to add a publication).

> The CMS edits **content**. The visual **design** (fonts, colors, spacing,
> layout) lives in the theme CSS (`assets/whl.css`) by design, so the site
> stays consistent.

**B. In code (for developers).** Edit the Markdown / YAML / Liquid files in this
repo and push. See §3–§4 below.

---

## 2. Repository layout

```
.
├── _config.yml                 ← Site configuration (heavily commented)
├── CNAME                       ← Custom domain (watershedhydrologylab.com)
├── CMS-SETUP.md                ← Sveltia CMS guide (editors + add-a-paper workflow)
├── DEPLOY.md / SETUP.md        ← Hosting + DNS wire-up notes
│
├── admin/                      ← Sveltia CMS (the browser content editor)
│   ├── index.html                 ← loads the CMS from its CDN
│   └── config.yml                 ← defines exactly what editors can change
│
├── _pages/                     ← Standalone pages (one file = one page)
│   ├── about.md                   ← Homepage  /            (layout: about)
│   ├── profiles.md                ← People    /people/     (layout: profiles)
│   ├── projects.md                ← Research index /projects/
│   ├── publications.md            ← Publications  /publications/
│   ├── facilities.md              ← Facilities    /facilities/
│   ├── contact.md                 ← Contact       /contact/
│   ├── news.md                    ← News          /news/
│   ├── cv.md  ·  404.md
│
├── _projects/                  ← One file per research theme (grid card + detail page)
│   ├── 1_hydrologic_modeling.md ·  2_ai_risk_mapping.md ·  3_decision_support.md
├── _news/                      ← One file per announcement (newest shown first)
├── _bibliography/papers.bib    ← Publications (BibTeX). Its header has the
│                                  step-by-step for adding a paper.
├── _data/socials.yml           ← Social / academic-profile links
│
├── _layouts/                   ← Local theme overrides
│   ├── about.liquid               ← homepage: hero (logo + title + CTAs) + pillars
│   ├── page.liquid                ← standard page; adds a cover-image hero and a
│   │                                "Related publications" section when set
│   └── profiles.liquid            ← people page
├── _includes/                  ← Local includes
│   ├── head.liquid                ← loads assets/whl.css + the web fonts
│   ├── header.liquid              ← branded navbar (logo + lab name)
│   └── whl_*.liquid               ← reusable content renderers (see §3)
│
├── assets/
│   ├── whl.css                    ← THE custom design system (earth-tone theme)
│   ├── img/team/                  ← member photos
│   ├── img/instruments/           ← Facilities sensor / lab-equipment photos
│   ├── img/affiliations/          ← affiliated-unit photos & logos (Contact)
│   ├── img/publication_preview/publications/  ← paper thumbnails
│   ├── img/research_*.jpeg        ← research-theme covers (cards + project hero + pillars)
│   ├── img/uploads/               ← images uploaded through the CMS
│   └── video/                     ← Field Gallery videos
│
├── .github/workflows/          ← CI (deploy.yml = build safety-net) + checks
├── Gemfile · Gemfile.lock       ← Ruby dependencies
└── package.json                 ← Node dependencies (build tooling)
```

Anything not listed is al-folio theme machinery you normally don't touch.

---

## 3. How the site is put together (for developers)

**Design system.** al-folio v1 ships its CSS pre-built from the `al_folio_core`
gem and does **not** recompile `assets/tailwind/app.css`, so all custom styling
lives in **`assets/whl.css`**, linked from the `_includes/head.liquid` override
(and kept outside `/assets/css/` so the purgecss step never strips it). It
overrides al-folio's `--global-*` variables for the matte earth-tone palette and
defines the lab's components (`.whl-card`, `.whl-btn`, `.whl-hero`, `.whl-map`,
`.whl-news`, etc.).

**Structured content via includes.** Instead of hand-written HTML in page
bodies, repeating UI is driven by front-matter data rendered through reusable
includes — this is what makes those parts editable in the CMS:

| Include                | Renders                                                                                   | Used by             |
| ---------------------- | ----------------------------------------------------------------------------------------- | ------------------- |
| `whl_buttons.liquid`   | a row of buttons from a list (mailto links are wrapped in Cloudflare `email_off` markers) | every page          |
| `whl_card_grid.liquid` | instrument / lab-equipment cards with photo(s)                                            | Facilities          |
| `whl_gallery.liquid`   | the Field Gallery (videos / photos / embeds)                                              | Facilities          |
| `whl_map.liquid`       | a Google-Maps embed built from a plain address                                            | Facilities, Contact |
| `whl_pi_card.liquid`   | the PI contact card                                                                       | Contact             |
| `whl_find_us.liquid`   | the RCREC building card + one card per affiliated unit                                    | Contact             |
| `whl_callout.liquid`   | a highlighted callout box (Markdown)                                                      | Contact, People     |
| `whl_alumni.liquid`    | the alumni photo grid                                                                     | People              |
| `whl_news.liquid`      | news as blocks (date + optional headline + photo + text); scrollable on the homepage      | Home, News          |

So, e.g., Facilities instruments live as an `instruments:` list in
`_pages/facilities.md` front matter and are rendered by
`{% include whl_card_grid.liquid items=page.instruments %}`.

**Research projects** set `img:` (the cover/banner — also drives the detail-page
hero) and `related_publications: true`; citing bib keys with
`{% cite key %}` in the body renders full publication cards
(thumbnail + DOI + link + citation) at the foot of the page.

---

## 4. Common edits in code

Most of these are also doable in the CMS (§1) — this is the code path.

- **Lab member** — add their photo to `assets/img/team/`, then add a block to
  the `profiles:` list in `_pages/profiles.md` (the bio is inline, in the `bio:`
  field; alternate `align: left` / `right`).
- **Publication** — see the step-by-step at the top of
  `_bibliography/papers.bib`; the copy-paste BibTeX template is in
  [`CMS-SETUP.md`](./CMS-SETUP.md) §5. Thumbnails go in
  `assets/img/publication_preview/publications/` (`preview = {publications/<file>.jpg}`).
- **News post** — add a file in `_news/` (`layout: post`, `date`, optional
  `headline:` and `image:`, then the text). Newest appears first.
- **Nav link** — in a page's front matter set `nav: true` and a `nav_order`
  (`title:` is the menu label).
- **Social / profile links** — `_data/socials.yml`.
- **Domain** — update `url:` in `_config.yml`, the `CNAME` file, and DNS.

---

## 5. Building locally (optional)

You only need this to preview before pushing. Requirements: Ruby + Bundler,
Node, and the gems in the `Gemfile`.

```bash
bundle install
npm install
bundle exec jekyll serve --livereload   # http://localhost:4000
```

Markdown edits hot-reload; `_config.yml` changes need a server restart.

---

## 6. Deployment

Every push to `main` triggers a **Cloudflare Pages** build: install toolchain →
`bundle exec jekyll build` → purge unused CSS → publish `_site/` to the CDN
behind `watershedhydrologylab.com`. The
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) workflow runs the
same build on GitHub Actions as a safety-net (no deploy). One-time wire-up
(build settings, env vars, DNS) is in [`DEPLOY.md`](./DEPLOY.md).

**Email links:** Cloudflare's _Email Address Obfuscation_ (Scrape Shield) would
rewrite `mailto:` links and break them, so every email is wrapped in
`<!--email_off-->…<!--/email_off-->` markers (emitted by the button / PI-card
includes), and `jekyll-minifier`'s `preserve_patterns` keeps those markers
through minification.

---

## 7. Credit & license

Built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme
(MIT license; preserved in `LICENSE`). Site content (text, photos, lab branding)
is © Watershed Hydrology Lab unless otherwise noted.
