# AGENTS.md — ofitec-landing

## Stack

- **Astro 2.x** (SSG, no SSR). TypeScript strict mode via `astro/tsconfigs/strict`.
- No UI framework integration (React, Vue, etc.) — components are `.astro` only.
- Styling: Bootstrap 5.3.1 via CDN + FontAwesome Pro 6 via CDN + Google Fonts via CDN. No local CSS framework install.
- No bundler config beyond `astro.config.mjs`. No PostCSS, Tailwind, or Sass.

## Commands

```bash
npm run dev       # Dev server at http://localhost:4321 (Astro 2.x default; README says 3000 but that's stale)
npm run build     # Output to ./dist/
npm run preview   # Serve dist/ locally
npm run deploy    # gh-pages -d dist  → deploys to Netlify? No — publishes dist/ to gh-pages branch
```

> **No test runner, no linter, no typecheck script defined.** `astro check` can be run manually: `npx astro check`.

## Project structure

```
src/
  layouts/Layout.astro   # Root shell: <html>, Navbar, Footer, WhatsApp float button, Bootstrap CDN tags
  components/            # Feature.astro, Footer.astro, Hero.astro, Navbar.astro, Section.astro
  pages/                 # index.astro, nosotros.astro, productos.astro  (file-based routing)
public/                  # Static assets served at root: images, SVGs, Empresas/ logos
```

## Conventions

- **Scoped styles** go inside the `.astro` file that uses them (Astro's default `<style>` scoping).
- **Global/shared styles** live in `Layout.astro`'s `<style>` block — `body`, `p`, WhatsApp float.
- Static images referenced in templates use root-relative paths (e.g. `/inicio.jpg`, `/Empresas/Trokelart.jpeg`). URLs with spaces must be percent-encoded (already the case in `index.astro`).
- `lang="esp"` is set on `<html>` — non-standard but intentional; don't change to `es` without checking with the owner.

## Deployment

- Production site: `https://ofitec.netlify.app` (set in `astro.config.mjs` as `site`).
- Deploy script (`npm run deploy`) pushes `dist/` to a `gh-pages` branch via the `gh-pages` package — this is separate from the Netlify deployment and may be legacy/unused. Clarify before running.

## Gotchas

- No `.env` file required; no environment variables used in the codebase.
- Bootstrap and FontAwesome are loaded from CDNs — no local install. Any icon or component usage depends on CDN availability.
- FontAwesome Pro CDN (`pro.fontawesome.com`) requires a valid kit/license for production. It may 403 without one.
- `dist/` and `.astro/` are gitignored — never commit them.
