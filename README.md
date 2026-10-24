# ScandinavianDev website

Source for [scandinavian.dev](https://scandinavian.dev): a mobile-first Jekyll
site for GitHub Pages, written in plain HTML and CSS (no Sass, no build tools
beyond Jekyll).

## Run locally

**With Docker / Dev Container** (VS Code): open the folder and choose
"Reopen in Container". The site runs at <http://localhost:4000> with live reload.

**With Ruby** (3.2+) and Bundler:

```bash
bundle install
bundle exec jekyll serve --livereload
```

Restart the server after changing `_config.yml`.

## Edit content

| What | Where |
| --- | --- |
| An offering (title, text, lists, illustration, CTA) | `_offerings/<name>.md` |
| Homepage hero and value props | `index.html` |
| Offerings intro / About & Contact page | `offerings.html`, `contact.html` |
| Calendly link, email, phone, address, legal details | `_config.yml` |
| Menu items | `_data/navigation.yml` |
| Button and label text ("What's included", etc.) | `_data/i18n/en.yml` |

**Add an offering:** copy a file in `_offerings/`, rename it (the filename
becomes the URL, e.g. `/offerings/new-thing/`), set `order` and `kind: supporting`.
Illustrations are inline SVG files in `_includes/illustrations/`; reference one
with `illustration: <file>.svg`, or use `image: /assets/images/<file>` for a
regular image.

**Add a language later:** copy `_data/i18n/en.yml` to `da.yml` / `sv.yml` and
translate; page content then gets translated copies under `/da/` and `/sv/`.

## Structure

```text
_config.yml              Site settings, Calendly, contact and legal details
_offerings/              One file per offering
_data/navigation.yml     Menu
_data/i18n/en.yml        UI strings
_layouts/                Page shell + offering template
_includes/               Header, footer, CTA band, offerings overview, icons
_includes/illustrations/ Inline SVG illustrations
_includes/css/           CSS partials (tokens, base, layout, components, sections)
assets/css/main.css      Joins the CSS partials into one file at build time
assets/js/main.js        Mobile menu
assets/images/           Hero image, favicon
```

## Old URLs

Pages from the previous Danish/English/Swedish site redirect to their closest
new page (`redirect_from` in each page's front matter), so existing links and
search results keep working.

## Deploy

GitHub Pages builds the site on every push to `main`. `CNAME` points it at
scandinavian.dev.
