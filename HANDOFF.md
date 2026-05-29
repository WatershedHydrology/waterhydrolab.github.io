# Ownership Handoff Runbook

Move ownership of the Watershed Hydrology Lab website to the **PI's institutional
email** (Dr. Golmar Golmohammadi), so the site is not tied to a personal account.

**Current phase:** keep the domain at **GoDaddy** for now (it's < 60 days old, so
an ICANN registrar-transfer is still locked); **consolidate the domain into
Cloudflare after the 60-day lock** (Phase 6).

> Companion doc: `CMS-SETUP.md` explains how the GitHub → Cloudflare → CMS pieces
> fit together. This file is the step-by-step transfer checklist.

**Legend:** **[PI]** = the professor does it · **[Dev]** = you (developer) do it ·
**[Both]** = one starts, the other confirms.

**Before you start**
- Keep all logins in the lab's password manager. **Never send a password or
  secret by email.**
- Follow the order below — done in this sequence, the live site stays up.
- The PI's **institutional email** is the anchor for every new account.

---

## What "the website" is (the pieces being transferred)

| Piece              | Today                                              | Goes to                                  |
| ------------------ | -------------------------------------------------- | ---------------------------------------- |
| Code (GitHub)      | `HugoMachadoRodrigues/waterhydrolab.github.io`     | Org `waterhydrolab` (PI-owned)           |
| Hosting (Cloudflare Pages) | builds + publishes on every push           | same account, PI added as Super Admin    |
| Domain             | `watershedhydrologylab.com` — **GoDaddy** (personal) | PI's GoDaddy account (Cloudflare later)  |
| CMS login (Sveltia)| GitHub OAuth App + Worker `sveltia-cms-auth…`      | OAuth App under the org; Worker in place |

---

## Phase 0 — The PI creates 3 accounts (all with the institutional email + 2FA)

- [ ] **[PI] GitHub** — <https://github.com/signup> → verify email → enable 2FA (*Settings → Password and authentication*).
- [ ] **[PI] Cloudflare** — <https://dash.cloudflare.com/sign-up> → verify → enable 2FA.
- [ ] **[PI] GoDaddy** — <https://www.godaddy.com> → create account → verify → enable 2FA.

## Phase 1 — GitHub: create the org and transfer the code

- [ ] **[PI]** GitHub → "**+**" (top-right) → **New organization** → **Free** plan → name `waterhydrolab`.
- [ ] **[PI]** Org → **People → Invite member** → the dev's username → role **Owner** (so the dev keeps maintaining).
- [ ] **[Dev]** Repo → **Settings → Danger Zone → Transfer** → new owner = `waterhydrolab` → confirm by typing the repo name.
- [ ] **[PI]** Accept the transfer. Repo becomes `waterhydrolab/waterhydrolab.github.io` (old URL redirects).
- [ ] **[Dev]** *(check)* If any workflow uses **Secrets** (*Settings → Secrets and variables → Actions*), re-add them — secrets don't move with a transfer.

## Phase 2 — Cloudflare: give the PI control (no infra change → zero downtime)

- [ ] **[Dev]** Cloudflare → **Manage Account → Members → Invite** → PI's institutional email → role **Super Administrator**.
- [ ] **[PI]** Accept the invite and log in — now controls Pages, DNS, and the Worker.
- [ ] **[Both]** *(optional)* Rename the account to "Watershed Hydrology Lab".

> We do **not** move the DNS zone or the Worker now — that's what avoids a
> nameserver change. Full consolidation is Phase 6.

## Phase 3 — Reconnect the build (Cloudflare Pages ↔ the org repo)

- [ ] **[Both]** Give Cloudflare access to the repo under its new owner:
  - GitHub → **Org `waterhydrolab` → Settings → GitHub Apps (Installed apps) → Cloudflare Pages → Configure** → grant the repo.
  - Cloudflare → **Workers & Pages → (the site project) → Settings → Builds & deployments** → confirm/reconnect to the org repo.
- [ ] **[Dev]** Test: make any commit (or "Retry deployment") → confirm it publishes in ~5 min.

## Phase 4 — GoDaddy: move the domain to the PI's account (DNS unchanged)

- [ ] **[Dev]** GoDaddy → **Domain Portfolio** → `watershedhydrologylab.com` → **⋯ → Move to another account** (Account Change) → enter the PI's institutional email.
- [ ] **[PI]** Accept the account move. Nameservers still point to Cloudflare → **site stays up**.
- [ ] **[PI]** Turn on **auto-renew** + add a payment method (*Domain Settings → Auto-renew: On*).

## Phase 5 — Reconfigure the CMS login (Sveltia)

- [ ] **[PI]** Create an **OAuth App under the org**: GitHub → **Org → Settings → Developer settings → OAuth Apps → New OAuth App**:
  - **Application name:** `Watershed Hydrology Lab CMS`
  - **Homepage URL:** `https://watershedhydrologylab.com`
  - **Authorization callback URL:** *(same as today)* `https://sveltia-cms-auth.rcrechydrologymactwo.workers.dev/callback`
  - Generate **Client ID** + **Client Secret** (copy the secret immediately).
- [ ] **[Both]** Cloudflare → **Workers & Pages → sveltia-cms-auth → Settings → Variables and Secrets**: set `GITHUB_CLIENT_ID` and `GITHUB_CLIENT_SECRET` (new), keep `ALLOWED_DOMAINS=watershedhydrologylab.com` → **Deploy**.
- [ ] **[Dev]** Update `admin/config.yml` → `backend.repo: waterhydrolab/waterhydrolab.github.io` (the Worker `base_url` does **not** change). Also update any other reference to the old username in the repo.
- [ ] **[PI]** Open `https://watershedhydrologylab.com/admin/` → log in with the PI's account → save a test edit.
- [ ] **[Dev]** Once it works: **regenerate the Client Secret** and **delete the old OAuth App** (the one on the personal account).

## ✅ Final verification

- [ ] Site loads normally at `watershedhydrologylab.com`.
- [ ] A push to the org repo publishes in ~5 min.
- [ ] `/admin/` logs in with the PI's account and saves a test edit.
- [ ] Domain shows in the **PI's** GoDaddy account, auto-renew ON.
- [ ] Dev remains **Owner** of the org and **Super Admin** in Cloudflare.

## Phase 6 — After 60 days: consolidate the domain into Cloudflare

- [ ] **[Both]** GoDaddy: **unlock** the domain + get the **EPP/authorization code**.
- [ ] **[PI]** Cloudflare (her account) → **Domain Registration → Transfer Domains** → follow the flow (~US$10, adds +1 year) → confirm by email → ~5 days.
- [ ] Result: registration + DNS + hosting all in one Cloudflare account.

---

## Notes & decisions

- **Cloudflare (Phase 2):** adding the PI as **Super Administrator** gives full
  control with no downtime. If you ever want a Cloudflare account created *fresh*
  under the PI's email (instead of co-administering the current one), that's
  possible but involves moving the DNS zone (a nameserver change) — plan it as a
  separate maintenance step.
- The Worker subdomain (`sveltia-cms-auth.rcrechydrologymactwo.workers.dev`) keeps
  working; it's cosmetic and can be re-deployed under a cleaner account later (then
  update `base_url` in `admin/config.yml` **and** the OAuth App callback to match).
- **GitHub Org Free** ($0) covers everything here; because the repo is **public**,
  GitHub Actions minutes are unlimited. The only recurring cost is the domain's
  annual renewal.
