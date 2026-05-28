# Setup guide — first-time deployment

This document walks through the one-time steps to get the
**Watershed Hydrology Lab** website live at
[watershedhydrologylab.com](https://watershedhydrologylab.com).

Read it from top to bottom; each section depends on the previous one.

> **Convention.** Lines starting with `$` are shell commands. Run them
> in a terminal opened inside the website folder on your computer
> (the one this README lives in).

---

## 0. Clean up two leftover files

Before doing anything else, delete these two items from this folder
(use Finder/Explorer — they were created during scaffolding and can't be
removed from inside the assistant's sandbox):

- `git_leftover_DELETE_ME/` ← old, partial `.git` folder
- `TEST_DELETE_ME.txt` ← empty test file

Once those are gone, continue.

---

## 1. Create the GitHub account and repository

### 1.1 GitHub account

Sign up at <https://github.com/signup> with the username **`waterhydrolab`**
(the username chosen for this lab). Use the lab's email if you have one
dedicated to public channels; otherwise use Dr. Golmohammadi's UF email.

Enable two-factor authentication: <https://github.com/settings/security>.

### 1.2 Repository

Create a new repository at <https://github.com/new>:

| Field             | Value                         |
| ----------------- | ----------------------------- |
| Owner             | `waterhydrolab`               |
| Repository name   | `waterhydrolab.github.io`     |
| Visibility        | **Public**                    |
| Initialize README | **No** (we already have one)  |
| .gitignore        | None                          |
| License           | None (we keep al-folio's MIT) |

> **Why this repo name?** A repository named exactly
> `<username>.github.io` is treated as the user's "personal site" by
> GitHub Pages. With a custom domain, the repo name doesn't strictly
> matter, but this convention makes the GitHub-served fallback URL
> (`waterhydrolab.github.io`) work without extra configuration.

Click **Create repository**. Leave the page open — you'll need the
`git remote add` command from the "…or push an existing repository"
section.

---

## 2. Push this code to GitHub

Open Terminal (macOS) or PowerShell (Windows) in the folder this README
is in.

```bash
# 1. Initialise the local repo
$ git init
$ git branch -M main

# 2. Stage and commit every file in the project
$ git add .
$ git commit -m "Initial site scaffold (al-folio theme, lab content)"

# 3. Hook the local repo up to GitHub. Replace the URL if you used a
#    different repo name.
$ git remote add origin https://github.com/waterhydrolab/waterhydrolab.github.io.git

# 4. Push
$ git push -u origin main
```

On the first push, GitHub may ask you to authenticate. The easiest way
is via the [GitHub CLI](https://cli.github.com/): install it, run
`gh auth login`, and then re-run `git push`. Alternatively, generate a
[Personal Access Token](https://github.com/settings/tokens) and use it
as your password.

---

## 3. Enable GitHub Pages

After the first push, the `deploy.yml` workflow will run automatically.
You can watch it at:

`https://github.com/waterhydrolab/waterhydrolab.github.io/actions`

The first run will:

1. Build the Jekyll site.
2. Create a new branch called `gh-pages` with the built site.

Once the workflow succeeds, configure Pages:

1. Go to
   <https://github.com/waterhydrolab/waterhydrolab.github.io/settings/pages>.
2. Under **Build and deployment**:
   - **Source:** _Deploy from a branch_
   - **Branch:** `gh-pages` / `/ (root)`
3. Click **Save**.

GitHub will publish the site within ~1 minute. You can preview it at
<https://waterhydrolab.github.io> before the custom domain is connected.

---

## 4. Connect the custom domain

You said you've purchased **watershedhydrologylab.com**. Here's how to
hook it up.

### 4.1 DNS records (at your domain registrar)

Log in to wherever you bought the domain (GoDaddy, Namecheap, Google
Domains / Squarespace, etc.) and add the following records to its DNS
zone:

#### Apex domain → GitHub Pages IPs (A records)

| Type | Host / Name | Value           | TTL  |
| ---- | ----------- | --------------- | ---- |
| A    | @           | 185.199.108.153 | 3600 |
| A    | @           | 185.199.109.153 | 3600 |
| A    | @           | 185.199.110.153 | 3600 |
| A    | @           | 185.199.111.153 | 3600 |

#### `www` subdomain → CNAME

| Type  | Host / Name | Value                   | TTL  |
| ----- | ----------- | ----------------------- | ---- |
| CNAME | www         | waterhydrolab.github.io | 3600 |

These records are from GitHub's official guide
([Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)).
Save the changes. DNS propagation can take from a few minutes to a few
hours.

### 4.2 Configure the domain in GitHub Pages

Back at
<https://github.com/waterhydrolab/waterhydrolab.github.io/settings/pages>:

1. Under **Custom domain**, enter `watershedhydrologylab.com` and click
   **Save**.
   _(The `CNAME` file in the repo already contains this value, so GitHub
   will detect it automatically as soon as DNS resolves.)_
2. Wait for the green DNS-check banner.
3. Tick **Enforce HTTPS** once it becomes available (a few minutes after
   the DNS check passes).

The site will now be live at
[https://watershedhydrologylab.com](https://watershedhydrologylab.com).

---

## 5. Connect the lab to its external profiles

The site already links to these. What follows is the one-time set-up
that lives **outside** the website.

| Service            | What to do                                                                                                                                                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **X / Twitter**    | Ensure `@WaterHydroLab` is current. Add a link back to `watershedhydrologylab.com` in the X bio and pinned tweet.                                                                                                               |
| **LinkedIn**       | Create a LinkedIn **Company / Showcase page** for the lab if you want a separate presence from the PI's personal profile. Add the website link there. Update `linkedin_username` in `_data/socials.yml` once you have the slug. |
| **GitHub**         | The org is `waterhydrolab`. Future code releases (models, scripts) can live as additional repos under this org and be linked from the site.                                                                                     |
| **Google Scholar** | Open Dr. Golmohammadi's Scholar profile, copy the value of the `user=` parameter in the URL, and confirm it matches the `scholar_userid: cpXxmlYAAAAJ` line in `_data/socials.yml`. If different, update the file.              |
| **ORCID**          | Confirmed: `0000-0001-5532-3892`. The ORCID profile should mention the lab website under "Websites".                                                                                                                            |
| **ResearchGate**   | Confirmed slug: `Golmar-Golmohammadi`. Add `watershedhydrologylab.com` to the profile's "Introduction" section.                                                                                                                 |
| **Scopus**         | Find Dr. Golmohammadi's Scopus Author ID by searching <https://www.scopus.com/freelookup/form/author.uri>. Add the URL to `_data/socials.yml` once you have it.                                                                 |
| **PubMed**         | PubMed indexes authors by an `Author Search` URL. Not strictly necessary for hydrology, but you can add the link as a custom_social entry if desired.                                                                           |

Connecting these profiles to the website is one-way (we link **out**
from the site to them) **and** two-way only if you also paste the
website URL into each external profile. Doing both helps with name
disambiguation and SEO.

---

## 6. Optional but recommended

- **Google Analytics.** Create a property at
  <https://analytics.google.com>, copy the `G-XXXXXXXXXX` measurement
  ID, and paste it in `_config.yml` under
  `analytics: → google:`. Commit and push.
- **Google Search Console.** Verify ownership at
  <https://search.google.com/search-console/> using the HTML meta tag
  method. Paste the verification ID into `_config.yml` under
  `google_site_verification:` and set
  `enable_google_verification: true`. Submit the sitemap at
  `https://watershedhydrologylab.com/sitemap.xml`.
- **Disable noisy GitHub Actions workflows.** The repo ships with
  several optional al-folio workflows (axe accessibility scan, broken
  link checker, Lighthouse, Prettier comment, etc.). They're useful but
  can be loud on PRs. To turn one off, open the file under
  `.github/workflows/` and add a `workflows: []` entry at the top, or
  delete the file outright. Do **not** touch `deploy.yml` — it's the
  one that publishes the site.
- **Branch protection.** In repo settings → branches, protect `main` to
  require PRs and at least one approving review before merging.

---

## 7. Day-to-day workflow

Once everything is set up, updating the site is just:

```bash
$ git pull          # get the latest version
$ git add -A
$ git commit -m "Add new publication, update Saba's bio"
$ git push          # deploy goes live ~2 minutes later
```

If you'd rather edit through the GitHub web UI, every file has a pencil
icon in the upper right when you open it on github.com — clicking it
opens an in-browser editor that commits directly to `main`.

---

## 8. Help and troubleshooting

- **Build failed?** Click into the failed run at
  `https://github.com/waterhydrolab/waterhydrolab.github.io/actions`.
  The error is usually shown in the last few lines of the "Install and
  Build" step. Common causes:
  - Malformed YAML front matter (missing `---`, wrong indentation).
  - BibTeX entry with a duplicate citekey.
  - Image path with a typo.
- **Site shows but custom domain isn't HTTPS yet?** Wait a few more
  minutes for GitHub to provision the certificate. If after an hour
  the "Enforce HTTPS" checkbox is still greyed out, remove the custom
  domain from Pages settings, save, re-add it, and save again.
- **al-folio documentation.** The original theme docs live in the
  `docs/` folder of this repo and at
  <https://github.com/alshedivat/al-folio>.

When in doubt, post a question in the al-folio GitHub Discussions:
<https://github.com/alshedivat/al-folio/discussions>.
