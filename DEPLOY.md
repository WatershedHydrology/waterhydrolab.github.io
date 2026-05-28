# Deploy guide — Cloudflare Pages

The live site at <https://watershedhydrologylab.com> is built and
served by **Cloudflare Pages**, connected to this GitHub repository.
Every push to `main` triggers a new production build; every pull
request gets its own preview URL.

The companion GitHub Actions workflow
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) runs the
same build in parallel as a CI safety-net — if the build breaks there,
the PR is blocked before Cloudflare even tries.

---

## 1. One-time setup in the Cloudflare dashboard

> You only do this once, when the repository is first connected.

1. Open <https://dash.cloudflare.com/> → **Workers & Pages** →
   **Create application** → **Pages** → **Connect to Git**.
2. Authorize Cloudflare on the `waterhydrolab` GitHub account and pick
   this repository.
3. Configure the build:

   | Field                      | Value                                                                                                                                                 |
   | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
   | **Project name**           | `watershedhydrologylab`                                                                                                                               |
   | **Production branch**      | `main`                                                                                                                                                |
   | **Framework preset**       | `Jekyll` (or `None` — the build command below overrides it)                                                                                           |
   | **Build command**          | `pip install --upgrade nbconvert && bundle install && npm ci && JEKYLL_ENV=production bundle exec jekyll build && npx purgecss -c purgecss.config.js` |
   | **Build output directory** | `_site`                                                                                                                                               |
   | **Root directory**         | leave empty (the repo root **is** the project root)                                                                                                   |
   | **Build system version**   | `2` (latest)                                                                                                                                          |

4. Open **Settings → Environment variables → Production** and add:

   | Variable         | Value        | Why                                         |
   | ---------------- | ------------ | ------------------------------------------- |
   | `RUBY_VERSION`   | `3.3.5`      | Matches CI; the gems pin to this minor.     |
   | `NODE_VERSION`   | `20.18.1`    | LTS Node 20. Used by `npm ci` and purgecss. |
   | `PYTHON_VERSION` | `3.13.1`     | Needed for `nbconvert` (jupyter notebooks). |
   | `JEKYLL_ENV`     | `production` | Triggers minifier + production CSS branch.  |

   Cloudflare Pages also reads `.tool-versions` from the repo as a
   fallback. The env-var pins above are stronger and survive editing
   that file accidentally.

5. **Add the custom domain** at **Settings → Custom domains →
   Set up a custom domain**:
   - Enter `watershedhydrologylab.com` (apex).
   - Cloudflare will either:
     - Tell you to delegate the domain (move the nameservers to
       Cloudflare at the registrar) — see § 2 below; or
     - Auto-create the records if the domain is already on Cloudflare.
   - Repeat with `www.watershedhydrologylab.com` and set it to redirect
     to the apex (in **Rules → Redirect Rules**).

6. SSL/TLS: in the dashboard set **SSL/TLS → Overview → Encryption
   mode** to **Full (strict)** once the domain is delegated. Cloudflare
   provisions the certificate automatically.

After step 5 is green, the site is live.

---

## 2. DNS — moving the domain to Cloudflare

The domain currently resolves to AWS IPs and uses GoDaddy nameservers
(`ns23/ns24.domaincontrol.com`). To use Cloudflare Pages with a custom
domain we need Cloudflare to be the **authoritative DNS** for the zone.

1. In Cloudflare dashboard → your account → **Add a site** →
   `watershedhydrologylab.com` → pick the Free plan.
2. Cloudflare scans existing DNS records (usually finds nothing useful
   from a parked AWS page — that's fine). Cloudflare hands you two
   nameserver names like `kim.ns.cloudflare.com` and
   `walt.ns.cloudflare.com`.
3. Go to your registrar (GoDaddy) → **Manage DNS** for the domain →
   **Nameservers → Change** → enter Cloudflare's two nameservers and
   save. Propagation: usually under an hour, up to 24 h.
4. Once Cloudflare shows the zone as **Active**, finish step 5 of § 1
   above to attach the Pages project to the domain.

> If the Cloudflare dashboard URL you have
> (`dash.cloudflare.com/.../watershedhydrologylab.com`) already shows
> the zone as **Active**, skip ahead — the only remaining task is
> attaching the Pages project under **Custom domains**.

---

## 3. What lives where (so you don't get confused)

| Concern             | Owned by                                                                 |
| ------------------- | ------------------------------------------------------------------------ |
| Source of truth     | GitHub repo (`main`)                                                     |
| Build (Jekyll)      | Cloudflare Pages                                                         |
| CDN + SSL           | Cloudflare                                                               |
| DNS                 | Cloudflare (after § 2)                                                   |
| Domain registration | GoDaddy (only the registrar, no nameservers needed there once delegated) |
| CI build-check      | GitHub Actions                                                           |
| Issue tracker       | GitHub                                                                   |

---

## 4. Day-to-day: how a change goes live

```
$ git pull                                # get latest main
$ # edit Markdown, push images, etc.
$ git add -A
$ git commit -m "Add 2026 publication, refresh team photo"
$ git push                                # triggers Cloudflare Pages deploy
```

Within ~2 minutes Cloudflare finishes the build and the site updates.
You'll see the deploy in the dashboard under **Workers & Pages →
watershedhydrologylab → Deployments**.

For preview deploys: open a PR. Cloudflare comments on the PR with a
unique URL like `abc1234.watershedhydrologylab.pages.dev` that you can
share with the team for review before merging.

---

## 5. Troubleshooting

- **Build fails with "bundler version mismatch"** — bump
  `RUBY_VERSION` to match Gemfile.lock's `BUNDLED WITH`.
- **`magick: command not found`** — ImageMagick is preinstalled in
  Cloudflare Pages v2. If a future runtime change removes it, add
  `apt-get install -y imagemagick` to the build command.
- **`nbconvert not found` during jupyter render** — confirm
  `PYTHON_VERSION` is set and the build command contains
  `pip install --upgrade nbconvert`.
- **Site builds but custom domain shows error 522/525** — DNS not
  delegated yet, or SSL mode mismatched. Set Cloudflare SSL to
  **Full (strict)** and wait for cert provisioning.
- **CSS looks broken in production** — purgecss removed a class it
  thought was unused. Add a safelist entry in `purgecss.config.js`.
