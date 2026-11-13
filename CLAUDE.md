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
- **Git:** `origin` = https://github.com/cipta77/til-site.git.
- **Secrets:** `.env.local` only holds a short-lived `VERCEL_OIDC_TOKEN`
  written by the Vercel CLI. Gitignored; never commit or print it.
- **Analytics:** none installed yet.

## Deploying

`vercel.json` sets framework `hugo`, build `hugo --minify`, output `public`,
and pins `HUGO_VERSION` (0.169.0) — Vercel builds the site itself.

```bash
vercel --prod      # deploy to production (omit --prod for a preview URL)
```

GitHub → Vercel auto-deploy is NOT connected yet (`vercel git connect`
failed: the Vercel account lacks access to cipta77/til-site). Until it is,
pushing does not deploy. Pushing to GitHub requires the `cipta77` gh account
(`gh auth switch -u cipta77`); switch back to `reon01425-glitch` afterwards.
On a new machine: `vercel login` then `vercel link` (pick `til-site`).

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
