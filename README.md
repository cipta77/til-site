# Today I Learned

A minimal personal TIL blog, built with [Hugo](https://gohugo.io), inspired
by [til.saugi.me](https://til.saugi.me/) (also a Hugo site).

## Adding a note

No code changes needed — just add a Markdown file:

```
hugo new posts/my-new-note.md
```

This creates `content/posts/my-new-note.md` with front matter already
filled in:

```
+++
date = '2026-11-01T12:00:00+07:00'
draft = false
title = 'My New Note'
tags = []
+++

Write the note here.
```

Set `tags` (e.g. `tags = ['python', 'debugging']`) and the note appears on
the home page and under `/tags/<tag>/` automatically on next build.

## Local preview

```
hugo server
```

Visit http://localhost:1313/. Pages reload live as you edit content.

## Build for deploy

```
hugo --minify
```

Outputs the static site to `public/`. Deploy that folder to any static
host (Netlify, GitHub Pages, Vercel, etc.). Set `baseURL` in `hugo.toml`
to your real domain before deploying.

## Structure

- `content/posts/` — your notes, one Markdown file per note
- `layouts/` — page templates (home list, single note, tag list)
- `static/css/style.css` — all styling, one file
- `hugo.toml` — site title, description, menu, tags config
