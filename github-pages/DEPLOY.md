# Deployment Guide — getanhourback.com

This folder contains everything needed for the GitHub Pages site.
When you're ready to go live, follow these steps in order.

---

## Step 1 — Create the GitHub Repository

1. Go to https://github.com/new
2. Repository name: `getanhourback.com`
3. Set to **Public** (required for free GitHub Pages)
4. Do NOT initialize with a README (you'll push these files directly)
5. Click **Create repository**

---

## Step 2 — Clone the Empty Repo via GitHub Desktop

Because this `github-pages` folder lives inside the `ripeda-ai-training` git repo, GitHub Desktop won't see it as its own repo. The cleanest fix: create the GitHub repo first, clone it to a fresh location on your Mac, then copy the files in.

1. Open **GitHub Desktop** → **File → Clone Repository…**
2. Find `ripeda/getanhourback.com` in the list (the repo you just created in Step 1)
3. Set the **Local Path** to somewhere outside the ai-training folder, e.g.:
   `~/Documents/GitHub/getanhourback.com`
4. Click **Clone**

---

## Step 3 — Copy the Deployment Files In

Open Finder and copy these 4 files from the `github-pages` folder into the freshly cloned folder:

- `index.html`
- `CNAME`
- `.nojekyll`
- `DEPLOY.md`

> **Tip:** `.nojekyll` is a dotfile and may be hidden in Finder. Press **⌘ + Shift + .** to toggle hidden files visible in Finder before copying.

Back in GitHub Desktop, you should now see all 4 files listed as new changes.

In the bottom-left summary field type `Initial deploy`, then click **Commit to main** → **Push origin**.

---

## Step 4 — Enable GitHub Pages

1. Go to the repo on GitHub → **Settings** → **Pages**
2. Under **Source**, select **Deploy from a branch**
3. Branch: `main`, Folder: `/ (root)`
4. Click **Save**
5. Under **Custom domain**, enter: `getanhourback.com`
6. Click **Save** — GitHub will verify the CNAME file automatically
7. Once DNS is configured and propagated, check **Enforce HTTPS**

Your site will be live at: `https://<username>.github.io/getanhourback.com` immediately,
and at `https://getanhourback.com` once DNS is set up.

---

## Step 5 — DNS Configuration for getanhourback.com (Primary)

Log into your domain registrar for **getanhourback.com** and add these records:

### A Records (apex domain — no www)
| Type | Host | Value | TTL |
|------|------|-------|-----|
| A | @ | 185.199.108.153 | 3600 |
| A | @ | 185.199.109.153 | 3600 |
| A | @ | 185.199.110.153 | 3600 |
| A | @ | 185.199.111.153 | 3600 |

### CNAME Record (www subdomain)
| Type | Host | Value | TTL |
|------|------|-------|-----|
| CNAME | www | ripeda.github.io | 3600 |

> Replace `ripeda.github.io` with your actual GitHub Pages subdomain if the repo is under a different account.

DNS propagation typically takes 15 minutes to a few hours. GitHub will automatically issue an SSL certificate once it detects the DNS records.

---

## Step 6 — Redirects for 1hourback.com and onehourback.com

For each of these two domains, log into their registrar and set up **URL forwarding / redirect**:

- **Destination:** `https://getanhourback.com`
- **Redirect type:** 301 (Permanent)
- **Forward path:** Yes (so any subpages redirect cleanly)

Most registrars have this under **Forwarding** or **URL Redirect** in the domain management panel. No hosting needed — the registrar handles it.

> If your registrar doesn't support URL forwarding, the easiest free alternative is to add the domain to a free Cloudflare account and set a **Page Rule** or **Redirect Rule** from `*1hourback.com/*` → `https://getanhourback.com`.

---

## Step 7 — Verify Everything Works

- [ ] `https://getanhourback.com` loads the page
- [ ] `https://www.getanhourback.com` loads the page (via CNAME → apex redirect GitHub handles)
- [ ] `https://1hourback.com` redirects to getanhourback.com
- [ ] `https://onehourback.com` redirects to getanhourback.com
- [ ] HTTPS lock icon is shown (no mixed content warnings)
- [ ] Page loads on mobile
- [ ] "Book a Free Discovery Call" button scrolls to CTA section
- [ ] Phone and email links work

---

## Files in This Folder

| File | Purpose |
|------|---------|
| `index.html` | The landing page (served as the homepage) |
| `CNAME` | Tells GitHub Pages to serve this site at `getanhourback.com` |
| `.nojekyll` | Prevents GitHub Pages from running Jekyll (not needed for plain HTML) |
| `DEPLOY.md` | This guide |

---

## Making Updates After Launch

Edit `index.html`, then in GitHub Desktop: write a commit message → **Commit to main** → **Push origin**. GitHub Pages redeploys automatically within ~1 minute.
