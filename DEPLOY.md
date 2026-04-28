# Fueller Site — Deployment Guide

The site uses **GitHub Pages** with the custom domain `fueller.app`.

---

## Step 1 — Create the GitHub repo

1. Go to [github.com/new](https://github.com/new)
2. Set the repo name to **`fueller-site`**
3. Set it to **Public** (required for free GitHub Pages)
4. Leave everything else as default and click **Create repository**

---

## Step 2 — Push the site files

From your local machine, in the folder containing these files:

```bash
git init
git add .
git commit -m "Initial holding page"
git branch -M main
git remote add origin https://github.com/GavT/fueller-site.git
git push -u origin main
```

> Replace `GavT` with your actual GitHub username if different.

---

## Step 3 — Enable GitHub Pages

1. In the repo, go to **Settings → Pages**
2. Under **Build and deployment**, set **Source** to `Deploy from a branch`
3. Set **Branch** to `main`, folder `/` (root)
4. Click **Save**

GitHub will confirm the site is publishing and show a URL like `https://GavT.github.io/fueller-site/`

---

## Step 4 — Point your DNS at GitHub

Log in to your domain registrar (wherever you manage `fueller.app`) and add the following DNS records:

### A records (apex domain)
| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

### CNAME record (www subdomain — optional but recommended)
| Type | Name | Value |
|------|------|-------|
| CNAME | www | GavT.github.io |

> DNS changes can take up to 48 hours to propagate, but usually much faster.

---

## Step 5 — Set the custom domain in GitHub Pages

1. Back in **Settings → Pages**
2. Under **Custom domain**, type `fueller.app` and click **Save**
3. Tick **Enforce HTTPS** once it becomes available (GitHub provisions a free Let's Encrypt cert automatically)

The `CNAME` file in the repo root does this automatically when you push, but confirming it in the UI locks it in.

---

## Updating the site

Any push to the `main` branch will automatically redeploy within ~1 minute. No build step needed — it's a plain HTML file.

```bash
# Make your edits to index.html, then:
git add index.html
git commit -m "Update holding page"
git push
```

---

## File structure

```
fueller-site/
├── index.html   # The holding page
└── CNAME        # Custom domain — do not delete this
```
