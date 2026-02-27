# Central Ohio Windows

## Project Overview

Lead-generation website for centralohiowindows.com that generates leads to sell to established window companies. Static site built with Astro.

## Tech Stack

- **Framework:** Astro v5 (static output mode)
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS v4 + daisyUI v5
- **SEO:** astro-seo + @astrojs/sitemap
- **Site URL:** https://centralohiowindows.com

## Key Architecture Decisions

- **Tailwind v4 via Vite plugin** (`@tailwindcss/vite`).
- **daisyUI v5 via CSS plugin** directive (`@plugin "daisyui"` in `src/styles/global.css`).
- **Static site generation** — no SSR, output is plain HTML/CSS/JS in `dist/`.

## Project Structure

```
src/
  layouts/BaseLayout.astro   # Base HTML layout with SEO and global CSS
  pages/                     # File-based routing (each .astro file = a page)
  styles/global.css          # Tailwind + daisyUI imports
public/                      # Static assets (favicons, etc.)
astro.config.mjs             # Astro config (Vite plugins, integrations, site URL)
tsconfig.json                # TypeScript strict config
```

## Commands

```bash
npm run dev       # Start dev server
npm run build     # Build static site to dist/
npm run preview   # Preview built site locally
```

## Conventions

- All pages should use `BaseLayout` and pass `title` (required) and `description` (required) props for SEO.
- Use Tailwind utility classes and daisyUI component classes for styling.
- No separate Tailwind or daisyUI config files — everything is configured via CSS in `src/styles/global.css`.
