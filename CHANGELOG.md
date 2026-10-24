# Changelog

All notable changes to the ScandinavianDev website.

## [Unreleased] – 2026-10-24 · Redesign (branch `redesign`)

Replaces the previous Danish/English/Swedish site with the new English design.

### Added

- New homepage: hero ("Security as a quality parameter"), core offering,
  supporting offerings and booking banner.
- Offerings overview page and one page per offering, all from a single template:
  - Product Security Engineering Training (core offering)
  - Security Champions Training
  - Tabletop Exercise Facilitation
  - Fractional CISO
  - Security Due Diligence for Growth
- About & Contact page with company story and legal information.
- Calendly booking on every call-to-action button.
- Sitemap-style footer.
- Inline SVG illustrations for the homepage and every offering page.
- SEO tags, `sitemap.xml`, `robots.txt` and a 404 page.
- Redirects from all previous DA/EN/SV URLs to their closest new page.
- UI text in `_data/i18n/en.yml`, ready for Danish and Swedish later.
- `.gitignore` for Jekyll build output.

### Changed

- Styling rewritten in plain, mobile-first CSS (no Sass), using the Inter font
  and a plain-text logo.
- Contact email is now info@scandinavian.dev.
- README rewritten as a guide for running, editing and deploying the site.
- Gemfile adds the `jekyll-seo-tag`, `jekyll-sitemap` and
  `jekyll-redirect-from` plugins (all on the GitHub Pages whitelist).

### Removed

- Previous Danish, English and Swedish pages, Sass files and data files.
- Unused images from the previous site.
- Committed `_site/` build output (now ignored).

### Kept

- `CNAME` (scandinavian.dev), `Dockerfile` and `.devcontainer/`.
