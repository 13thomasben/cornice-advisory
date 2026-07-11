# Deploying to GitHub Pages (free)

The entire website is the self-contained static file `client/public/site.html`.
The workflow in `.github/workflows/deploy-pages.yml` publishes it to GitHub
Pages as `index.html` on every push to `main` (or manually via the Actions tab
→ "Deploy to GitHub Pages" → Run workflow).

## One-time setup

1. **Make the repository public**: GitHub Pages is only free on public
   repositories. Go to **Settings → General → Danger Zone → Change repository
   visibility → Make public**. (The repo contains no secrets — only the
   website itself and UI boilerplate.) The workflow then enables Pages and
   sets the custom domain automatically on its next run.

2. **Point the domain at GitHub Pages** (at your DNS provider / registrar):
   - Apex `corniceadvisory.com` — add these `A` records:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
     (optionally `AAAA`: 2606:50c0:8000::153, :8001::153, :8002::153, :8003::153)
   - `www.corniceadvisory.com` — add a `CNAME` record pointing to
     `13thomasben.github.io`
   - Remove the old Manus DNS records for these names first.

3. **Enforce HTTPS**: the workflow sets the custom domain automatically. Once
   DNS has propagated and the certificate is issued (usually within an hour),
   tick **Enforce HTTPS** under **Settings → Pages**.

Until DNS is switched, the site is reachable at
`https://13thomasben.github.io/cornice-advisory/`.

## Updating the site

Edit `client/public/site.html` and push to `main` — the workflow redeploys
automatically.
