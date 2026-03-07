# mandrew.ai — Setup Guide

## 1. Create the GitHub Repo

```bash
# Create a new repo on GitHub (public or private — both work with Pages)
gh repo create mandrew-site --public --source=. --remote=origin --push
# OR just create it on github.com and push this folder to it
```

If you already have a repo, just copy all these files into it and push to `main`.

## 2. Enable GitHub Pages

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. That's it — the included workflow (`.github/workflows/deploy.yml`) handles deployment automatically on every push to `main`

## 3. Configure GoDaddy DNS

Log into [GoDaddy DNS Management](https://dcc.godaddy.com/dns) for **mandrew.ai** and set up these records:

### For the apex domain (mandrew.ai):

| Type  | Name | Value             | TTL    |
|-------|------|-------------------|--------|
| A     | @    | 185.199.108.153   | 600    |
| A     | @    | 185.199.109.153   | 600    |
| A     | @    | 185.199.110.153   | 600    |
| A     | @    | 185.199.111.153   | 600    |

### For the www subdomain:

| Type  | Name | Value                          | TTL    |
|-------|------|--------------------------------|--------|
| CNAME | www  | your-github-username.github.io | 600    |

> Replace `your-github-username` with your actual GitHub username.

## 4. Verify Custom Domain in GitHub

1. Go to your repo → **Settings** → **Pages**
2. Under **Custom domain**, enter `mandrew.ai`
3. Click **Save**
4. Wait for the DNS check to pass (can take a few minutes to a few hours)
5. Check **Enforce HTTPS** once it becomes available

## 5. Deploy

Every push to `main` will automatically deploy. To test:

```bash
git add .
git commit -m "Initial site"
git push origin main
```

The site will be live at **https://mandrew.ai** once DNS propagates (usually 15–60 minutes, can take up to 48 hours).

## File Structure

```
mandrew-site/
├── .github/
│   └── workflows/
│       └── deploy.yml      ← Auto-deploy on push
├── assets/                  ← Put images, CSS, JS here
├── .gitignore
├── CNAME                    ← Tells GitHub Pages your domain
├── index.html               ← The landing page
└── SETUP.md                 ← This file (safe to delete)
```
