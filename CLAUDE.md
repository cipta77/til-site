# CLAUDE.md

Personal portfolio + blog + TIL site for Cipta Fikri Wiratama ("fikriw"),
built with Hugo. Live at https://fikriw.fun/.

## Infrastructure

- **Hosting:** Vercel project `til-site` under team `reon01425-s-projects`
  (account `reon01425-glitch`). This dir is linked via `.vercel/project.json`.
- **Domain:** `fikriw.fun` → A record `76.76.21.21` (Vercel's anycast IP).
  DNS is managed at the registrar (nameservers `*.dns-parking.com`, likely
  Hostinger), not at Vercel.
- **No server / SSH / IP to manage** — it's a static site. Access = being
  logged in to the Vercel CLI (`vercel whoami`).
- **Git:** `origin` = https://github.com/cipta77/til-site.git. Git is NOT
  connected to Vercel — pushing does not deploy.
- **Secrets:** `.env.local` only holds a short-lived `VERCEL_OIDC_TOKEN`
  written by the Vercel CLI. Gitignored; never commit or print it.
- **Analytics:** none installed yet.

## Deploying

Vercel framework preset is "Other" with no build step; it serves the
locally built `public/` folder. Always build first:

```bash
hugo --minify      # builds into public/
vercel --prod      # deploy to production (omit --prod for a preview URL)
```

`vercel.json` pins `HUGO_VERSION` (0.169.0). On a new machine:
`vercel login` then `vercel link` (pick `til-site`).

## Adding content

```bash
hugo new posts/my-note.md   # TIL note  → /posts/
hugo new blog/my-post.md    # blog post → /blog/
hugo server                 # preview at http://localhost:1313/
```

Front matter (TOML): `title`, `date`, `draft = false`, `tags = ['x']`.
Tags auto-generate pages under `/tags/<tag>/`.

- Achievements / certificates / projects are data-driven: edit
  `data/achievements.yaml`, `data/certificates.yaml`, `data/projects.yaml`.
- About page text: `content/_index.md`. Contact: `content/contact.md`.
- Site params, menu, social links: `hugo.toml`.

## Code layout

- `layouts/` — templates (`_default/baseof.html` is the shell; per-section
  `list.html`/`single.html` for blog, achievements, certificates, projects)
- `layouts/partials/` — header, footer
- `static/css/style.css` — all styling in one file; light/dark theme via
  `data-theme` attribute on `<html>`, persisted in `localStorage`
- Goldmark `unsafe = true` — raw HTML allowed in Markdown
