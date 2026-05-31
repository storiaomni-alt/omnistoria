# OMNISTORIA — Deployment Package

This folder is ready to deploy to Cloudflare Pages, GitHub Pages, or Netlify.

## Files
- `index.html` — Main landing page (omnistoria.html renamed)
- `omnistoria-llm.html` — AI chat interface (calls Anthropic API)
- `_redirects` — Netlify routing rules
- `_headers` — Cloudflare Pages security headers
- `netlify.toml` — Netlify build config
- `.github/workflows/deploy.yml` — GitHub Actions auto-deploy

---

## Cloudflare Pages (drag-and-drop, no Git)

1. Go to https://pages.cloudflare.com → Create a project → Upload assets
2. Name your project (e.g. `omnistoria`)
3. Drag ALL files from this folder into the upload box
4. Click **Deploy site**
5. Your site is live at `omnistoria.pages.dev`

To add a custom domain: Dashboard → Custom domains → Add domain

---

## GitHub Pages (via Git)

```bash
# 1. Create a new repo on GitHub named: omnistoria-site

# 2. Push this folder
git init
git add .
git commit -m "deploy omnistoria"
git remote add origin https://github.com/YOUR_USERNAME/omnistoria-site.git
git push -u origin main

# 3. In repo Settings → Pages → Source: GitHub Actions
# The workflow in .github/workflows/deploy.yml handles the rest
```

Your site will be live at: `https://YOUR_USERNAME.github.io/omnistoria-site`

---

## Netlify (drag-and-drop, no Git)

1. Go to https://app.netlify.com → Add new site → Deploy manually
2. Drag this entire folder into the deploy box
3. Done — live at `random-name.netlify.app`

To rename: Site configuration → Change site name

---

## API Key Security (omnistoria-llm.html)

The LLM chat page calls the Anthropic API directly from the browser.
Before deploying publicly, either:

A) Add your key directly in the HTML (dev/private use only):
   Find `headers: {` and add:
   `'x-api-key': 'sk-ant-YOUR_KEY_HERE',`

B) Use a proxy (recommended for production):
   - Cloudflare Worker → Workers & Pages → Create Worker
   - Netlify Function → netlify/functions/proxy.js
   This keeps your key server-side and hidden from users.
