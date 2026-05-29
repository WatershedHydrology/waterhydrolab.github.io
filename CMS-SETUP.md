# Content Management (Sveltia CMS) — Setup & Operations Guide

This site can be edited from a browser by non-technical staff through
**[Sveltia CMS](https://github.com/sveltia/sveltia-cms)** — a fast, open-source,
**Decap-CMS-compatible** content manager.

- **Editor panel:** <https://watershedhydrologylab.com/admin/>
- **How it works:** the editor fills in forms; clicking **Save** commits the
  change to the GitHub repo (`WatershedHydrology/waterhydrolab.github.io`,
  branch `main`); **Cloudflare Pages** then rebuilds and publishes the site
  automatically (usually within ~5 minutes). Editors never touch code.

> The CMS edits **content** (text, images, items, ordering). The visual
> **design** (fonts, colors, sizes, spacing, layout) lives in the theme CSS
> (`assets/whl.css`) by design, so the site stays consistent.

---

## 1. Architecture

```
Editor's browser                GitHub repo                 Cloudflare
┌────────────────┐   commit    ┌──────────────────┐  push   ┌──────────────┐
│ /admin/        │ ──────────▶ │ waterhydrolab.   │ ──────▶ │ Pages build  │
│ (Sveltia CMS)  │             │ github.io (main) │         │ → publish    │
└──────┬─────────┘             └──────────────────┘         └──────────────┘
       │  OAuth login
       ▼
┌──────────────────────────────┐
│ sveltia-cms-auth Worker       │  (Cloudflare Worker — OAuth proxy to GitHub)
│ …workers.dev                  │
└──────────────────────────────┘
```

Two files in this repo drive the panel:

| File               | Purpose                                                                       |
| ------------------ | ----------------------------------------------------------------------------- |
| `admin/index.html` | Loads Sveltia CMS from its CDN.                                               |
| `admin/config.yml` | Defines the backend (GitHub), media folder, and the editable **collections**. |

---

## 2. One-time setup (already done — documented for the record)

Because the site is hosted on **Cloudflare Pages** (not Netlify), GitHub login
needs a small OAuth proxy. Three pieces:

### 2a. GitHub OAuth App

- Created at **GitHub → Settings → Developers → OAuth Apps**.
- **Application name:** `Watershed Hydrology Lab CMS`
- **Homepage URL:** `https://watershedhydrologylab.com`
- **Authorization callback URL:**
  `https://sveltia-cms-auth.rcrechydrologymactwo.workers.dev/callback`
- Produces a **Client ID** and a **Client Secret** (the secret is shown once —
  regenerate if lost).

### 2b. `sveltia-cms-auth` Cloudflare Worker (the OAuth proxy)

- Deployed from <https://github.com/sveltia/sveltia-cms-auth> ("Deploy to
  Cloudflare").
- Live URL: `https://sveltia-cms-auth.rcrechydrologymactwo.workers.dev`
- **Environment variables / secrets** (Worker → Settings → Variables and Secrets):

  | Name                   | Type                   | Value                                |
  | ---------------------- | ---------------------- | ------------------------------------ |
  | `GITHUB_CLIENT_ID`     | Text                   | _(Client ID from the OAuth App)_     |
  | `GITHUB_CLIENT_SECRET` | **Secret (encrypted)** | _(Client Secret from the OAuth App)_ |
  | `ALLOWED_DOMAINS`      | Text                   | `watershedhydrologylab.com`          |

  > Add other domains comma-separated if you ever want to log in from a
  > different host (e.g. a `*.pages.dev` preview).

### 2c. Point the CMS at the Worker

In `admin/config.yml`:

```yaml
backend:
  name: github
  repo: WatershedHydrology/waterhydrolab.github.io
  branch: main
  base_url: https://sveltia-cms-auth.rcrechydrologymactwo.workers.dev
```

---

## 3. Giving someone edit access

The GitHub backend lets anyone **with write access to the repo** save changes.

1. The person needs a free **GitHub account** (<https://github.com/signup>).
2. **GitHub → repo → Settings → Collaborators → Add people** → their username →
   role **Write**.
3. They **accept the email invitation**.
4. They can now sign in at `/admin/` and edit.

To revoke access, remove them from Collaborators.

---

## 4. What editors can change (collections)

Open <https://watershedhydrologylab.com/admin/> and pick a collection:

| Collection               | Edits                                                                                                                                                    |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Home page**            | Hero **subtitle** (rich text) & tagline, the three research pillars (add / edit / reorder), the PI photo + **contact card** (organization, address, phone, email), and the “About the Lab” text.                              |
| **News & Announcements** | Add / edit short announcements (homepage strip + News page).                                                                                             |
| **Research Projects**    | The research-theme cards (title, **cover / banner image**, description, order, full text, related publications).                                                                            |
| **Team / People**        | Members list — **drag to reorder**, swap **photo**, edit **Role / Focus / Joined** and **Bio** per member; alumni grid + “Join the lab” block via the body field. |
| **Other Pages**          | **Facilities** (instruments, lab equipment, Field Gallery, map, buttons), **Contact** (PI card, map, affiliations, buttons, callout), the **News** page, and the **Publications** page buttons. |
| **Downloads & QR codes** | Preview, download, or replace the QR codes and share cards (also on the site's **Downloads** page).                                                       |

### Adding images, maps, and videos — no HTML needed

- **Photo:** click the image button on any image field (uploads to
  `assets/img/uploads/`).
- **Map:** in the page's **Map** field, just type the **address** — the map
  builds itself (optional zoom, 1–20).
- **Video (Facilities → Field Gallery):** add a gallery item and either
  **upload** a video file, or paste a normal **YouTube/Vimeo link**
  (e.g. `https://youtu.be/abc123`) — the player is built for you.

### Everything is editable without HTML ✅

Every field is a **plain text box**, a **rich-text editor** (with a link
button), an **image / file picker**, or a **list** you add rows to. You never
type or paste HTML. Quick reference:

| To…                       | Where                                        | How (no HTML)                                       |
| ------------------------- | -------------------------------------------- | --------------------------------------------------- |
| Edit the hero subtitle    | Home → **Hero subtitle**                     | Type text; use the **link button** for links        |
| Edit the PI contact card  | Home → **Contact card**                      | Fill Organization / Address / Office / Phone / Email |
| Set a person's role       | People → a member                            | Fill the **Role**, **Focus**, **Joined** boxes      |
| Write a bio / About text  | People → Bio · Home → About                  | Rich-text editor (bold, links, lists)               |
| Add a photo               | any **image** field                          | Click → upload                                      |
| Add a map                 | Facilities / Contact → **Map**               | Type the **address**                                |
| Add a video               | Facilities → **Field Gallery**               | Upload a file, or paste a **YouTube/Vimeo link**    |
| Add a button              | any **Buttons** list                         | Fill Label + Link (+ optional icon)                 |
| Get a QR code             | **Downloads & QR codes** / site **Downloads** | Click **Download**                                  |

> The only "code-looking" lines are the `{% … %}` **include** lines at the
> bottom of a few page bodies (Facilities, Contact, News, Publications). They
> pull in the structured content above — **leave them exactly as they are.**
> They are not HTML and never need editing.
>
> The Research **index** grid and the page **design** (`_layouts/`, `_includes/`,
> `assets/whl.css`) live in code; research content itself is edited in the
> **Research Projects** collection.

---

## 5. Not in the CMS (edited in code)

- **Publications** (`_bibliography/papers.bib`) — BibTeX is not a CMS-friendly
  format, so papers are added in code. The top of `papers.bib` has the full
  step-by-step; the copy-paste **entry template** is shown below. In short:
  1. Get the BibTeX (publisher "Cite/Export", or paste the DOI into
     <https://www.doi2bib.org/>).
  2. Give it a citekey `lastnameYEARkeyword`; fill the template's `doi`, `html`
     (full-text URL), and optional `abstract`.
  3. Optional thumbnail: drop a JPG in
     `assets/img/publication_preview/publications/` and set
     `preview = {publications/<file>.jpg}`.
  4. Paste it under the right year in `papers.bib`, commit & push.
  5. To feature it on a Research project, add a `cite` tag for its citekey in
     that project's body (the projects already do this) — it renders as a full
     card (thumbnail + DOI + link + citation) at the foot of the page.

  **Copy-paste entry template** — fill it in and paste under the right year in
  `papers.bib`. Only `title`, `author`, `journal`, `year`, `doi`, and `html`
  are really needed; the rest are optional niceties.

  ```bibtex
  @article{lastname2026keyword,
    title       = {{Full Article Title — double braces keep the capitalization}},
    author      = {Lastname, F. M. and Golmohammadi, Golmar and Coauthor, A. B.},
    journal     = {Journal Name},
    year        = {2026},
    month       = {January},
    volume      = {0},
    number      = {0},
    pages       = {1--10},
    doi         = {10.xxxx/xxxxxx},
    html        = {https://publisher.com/full-text-url},
    preview     = {publications/your-thumbnail.jpg},
    abstract    = {One-paragraph summary shown on the paper's detail page.},
    selected    = {true},
    bibtex_show = {true},
    altmetric   = {true},
    dimensions  = {true}
  }
  ```

  - `title` — keep the **double braces** `{{ }}` so the journal's capitalization
    is preserved.
  - `author` — `Last, First M. and Last2, First2 and …`. Dr. **Golmohammadi,
    Golmar** is bolded automatically wherever she appears.
  - `doi` — the bare DOI (e.g. `10.3390/su17052250`), not a URL.
  - `html` — the publisher's full-text page URL.
  - `preview` — drop a ~600×400 JPG in
    `assets/img/publication_preview/publications/`, then reference it as
    `publications/<file>.jpg`.
  - `selected = {true}` — also lists the paper in the homepage "Selected" strip.
  - Drop `altmetric`/`dimensions` if the paper has no DOI.

- **Design / theme** (`assets/whl.css`, layouts in `_layouts/`, header/footer in
  `_includes/`) — changed by a developer to keep the look consistent.

---

## 6. Gotchas & troubleshooting

- **Login fails right after authorizing GitHub** → the `GITHUB_CLIENT_SECRET` on
  the Worker is wrong/missing, or the user lacks repo write access.
- **Login page never appears / "domain not allowed"** → `ALLOWED_DOMAINS` on the
  Worker must include the domain you are visiting. Use
  `watershedhydrologylab.com` (not the `*.pages.dev` URL).
- **`mailto:` buttons not opening an email?** Addresses entered in the CMS
  **Email** fields are rendered with Cloudflare "email_off" markers, so they
  stay clickable (not obfuscated) — you do **not** need to change any Cloudflare
  setting. If you ever hand-write an address somewhere else and it stops working,
  use the dedicated **Email** field instead; it's protected automatically.
- **A field disappears after an editor saves a page** → the page's front matter
  has a field not declared in `admin/config.yml`. Every structural field must be
  listed there (most are `hidden`) so Sveltia preserves it. Don't delete the
  `hidden` fields.
- **Edits don't appear on the live site** → check the Cloudflare Pages build
  status; a failed build won't publish. The GitHub Actions "Build (CI check)"
  validates the same build on every push.
- **Local editing without GitHub** (developers): run a local proxy and add
  `local_backend: true` to `admin/config.yml`, then `npx @sveltia/cms-proxy-server`.
