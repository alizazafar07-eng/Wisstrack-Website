# WissTrack Landing Page — GitHub Pages + GoDaddy domain

A static, single-file site (HTML/CSS/JS, no build step). This version is set up for
**GitHub Pages** hosting with your **GoDaddy domain** pointed at it.

---

## Step 1 — Edit the CNAME file

Open `CNAME` in this folder and replace `yourdomain.com` with your actual GoDaddy domain
(e.g. `wisstrack.com`, no `http://`, no trailing slash). Save it.

If you'd rather use a subdomain (e.g. `app.wisstrack.com`), put that instead.

## Step 2 — Push to GitHub

1. Go to https://github.com → **New repository** → name it anything, e.g. `wisstrack-landing-page`.
   Keep it **Public** (required for free GitHub Pages).
2. Upload all four files from this folder (`index.html`, `CNAME`, `.nojekyll`, `README.md`)
   using GitHub's **"uploading an existing file"** link on the repo's main page — no command
   line needed. Commit the upload.

## Step 3 — Turn on GitHub Pages

1. In your repo, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Click **Save**.
4. Under **Custom domain**, enter the same domain you put in the `CNAME` file and save.
   GitHub will show a message that DNS check is pending — that's expected until Step 4 is done.

## Step 4 — Point your GoDaddy domain at GitHub Pages

Log into GoDaddy → **My Products → DNS** (or **Manage DNS**) for your domain, and add these records.

**If using the root/apex domain (e.g. `wisstrack.com`):**

Add four **A** records, all with Host `@`, pointing to GitHub Pages' IP addresses:

| Type | Host | Value             | TTL     |
|------|------|--------------------|---------|
| A    | @    | 185.199.108.153    | 1 hour  |
| A    | @    | 185.199.109.153    | 1 hour  |
| A    | @    | 185.199.110.153    | 1 hour  |
| A    | @    | 185.199.111.153    | 1 hour  |

Also add, so `www` works too:

| Type  | Host | Value                        | TTL    |
|-------|------|------------------------------|--------|
| CNAME | www  | `<your-github-username>.github.io` | 1 hour |

**If using a subdomain instead (e.g. `app.wisstrack.com`):**

| Type  | Host | Value                        | TTL    |
|-------|------|------------------------------|--------|
| CNAME | app  | `<your-github-username>.github.io` | 1 hour |

(GoDaddy may already have a default "Parked" A record or forwarding rule on `@` — delete
that first so it doesn't conflict.)

## Step 5 — Wait for DNS + enable HTTPS

- DNS changes can take anywhere from a few minutes to a few hours to propagate.
- Once GitHub's Pages settings page shows the domain as verified (green check), tick
  **Enforce HTTPS** in the same Settings → Pages screen. GitHub issues a free SSL certificate
  automatically.

Your site will then be live at `https://yourdomain.com`.

---

## Editing later

The whole site is one file, `index.html` — everything (CSS, JS) is inline. Edit it, upload the
new version to the same repo (or push via git), and GitHub Pages redeploys automatically within
a minute or two.
