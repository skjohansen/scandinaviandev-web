# ScandinavianDev website

Source for [scandinavian.dev](https://scandinavian.dev): a mobile-first Jekyll
site hosted on GitHub Pages, written in plain HTML and CSS. No Sass, no
JavaScript framework and no build tools beyond Jekyll.

- [Run locally](#run-locally)
- [Edit content](#edit-content)
- [Add an offering](#add-an-offering)
- [Illustrations and images](#illustrations-and-images)
- [Styling](#styling)
- [Add Danish and Swedish later](#add-danish-and-swedish-later)
- [Old URLs and redirects](#old-urls-and-redirects)
- [Deploy](#deploy)
- [Project structure](#project-structure)

## Run locally

**Option 1: Dev Container (VS Code, recommended).** Open the folder in VS Code
and choose **Reopen in Container**. The site starts automatically at
<http://localhost:4000> with live reload.

**Option 2: Ruby** (3.2 or newer) and Bundler:

```bash
bundle install
bundle exec jekyll serve --livereload
```

Open <http://localhost:4000>. Restart the server after changing `_config.yml`.

**Option 3: Docker (production-like build served by nginx):**

```bash
docker build -t scandinaviandev .
docker run --rm -p 8080:80 scandinaviandev
```

Open <http://localhost:8080>.

## Edit content

Most text lives in a few files, so you rarely need to touch the HTML.

| What | Where |
| --- | --- |
| Homepage hero, value props | `index.html` |
| Offerings overview ("Five offerings, one path") intro | `offerings.html` |
| Each offering page (text, lists, illustration, call to action) | `_offerings/<name>.md` |
| About & Contact page text | `contact.html` |
| Calendly link | `_config.yml` → `calendly_url` |
| Email, phone, address | `_config.yml` → `contact` |
| Company name, org. number, VAT, CEO | `_config.yml` → `legal` |
| Site title, SEO description | `_config.yml` → `title`, `description` |
| Menu items | `_data/navigation.yml` |
| Button and label text ("What's included", "Schedule via Calendly", etc.) | `_data/i18n/en.yml` |

Every "Book an intro call" and "Schedule via Calendly" button uses
`calendly_url`, so changing it there updates the whole site.

## Add an offering

1. Copy an existing file in `_offerings/`, for example
   `_offerings/security-champions.md`, and rename it. The filename becomes the
   URL: `_offerings/new-thing.md` → `/offerings/new-thing/`.
2. Edit the front matter:
   - `order`: position in lists (1 = first)
   - `kind`: `supporting` (exactly one offering is `core`; it gets the large
     block on the homepage)
   - `eyebrow`, `title`, `lead`, `included`, `audience`, `decision_makers`
   - `card_title`, `card_tag`, `card_text`: the card on the homepage
   - `cta_title`, `cta_text`: the dark banner at the bottom of the page
   - `path_step`, `path_title`, `path_text`, `path_icon`: the step on the
     offerings overview page (icons live in
     `_includes/illustrations/offering-icons.svg`; the wide desktop
     illustration is `_includes/illustrations/offerings-path.svg`)
   - `illustration` or `image`: see below
3. Save. The homepage, offerings overview, footer and "Other offerings" links
   pick it up automatically.

## Illustrations and images

The offering illustrations are **inline SVG** files in
`_includes/illustrations/`. They stay sharp on every screen and add almost
nothing to page weight. Use one with:

```yaml
illustration: fractional-ciso.svg
```

To use a regular image instead, put it in `assets/images/` and use:

```yaml
image: /assets/images/my-illustration.jpg
image_alt: Short description of the image
```

Recommended size for images: at least 1600 px wide, 4:3 ratio, JPG or WebP
under ~250 KB.

The homepage hero image is `assets/images/hero-scandinavia.jpg`.

### Logo and icons

| File | Used for |
| --- | --- |
| `_includes/logo-mark.svg` | Shield logo in the header (inline; colour follows the site blue) |
| `assets/images/logo-mark.svg` | Standalone vector logo |
| `assets/images/favicon.svg`, `favicon.png` | Browser tab icon |
| `assets/images/apple-touch-icon.png` | iPhone/iPad home screen icon |
| `assets/images/logo-512.png` | Logo for search engines |
| `assets/images/og-image.png` | Share thumbnail (LinkedIn, Slack, etc.), 1200×630 |

The share thumbnail is set for every page in `_config.yml` (`defaults` →
`image`). A page can use its own by setting `image:` in its front matter.

## Styling

CSS is plain CSS split into small files in `_includes/css/`. Jekyll joins them
into one file (`assets/css/main.css`) at build time.

| File | Contains |
| --- | --- |
| `tokens.css` | Colours, font sizes, spacing. Change the look here first. |
| `base.css` | Reset and base typography |
| `layout.css` | Container, header, footer |
| `components.css` | Buttons, labels, cards, call-to-action banner |
| `sections.css` | Hero, offering pages, About & Contact |

The layout is mobile-first: base styles are for phones, and larger screens
are handled with `min-width` media queries (768 px, 1024 px, 1280 px, 1600 px).
There are no animations or transitions, by design.

## Add Danish and Swedish later

The site is prepared for more languages:

1. Copy `_data/i18n/en.yml` to `_data/i18n/da.yml` and `sv.yml` and translate
   the button and label text.
2. Create translated copies of the pages under `/da/` and `/sv/` (and the
   offerings), each with `lang: da` or `lang: sv` in the front matter.
3. Switch the language lookup in the templates from `site.lang` to
   `page.lang | default: site.lang`, and add a language switcher to the header.

## Old URLs and redirects

Pages from the previous Danish/English/Swedish site redirect to their closest
new page, so existing links and search results keep working. Redirects are
listed under `redirect_from` in each page's front matter.

| Old URL | Now goes to |
| --- | --- |
| `/en/`, `/sv/` | `/` |
| `/tjenester/`, `/en/services/`, `/sv/tjanster/` | `/offerings/` |
| `/kompetencer/`, `/en/competencies/`, `/sv/kompetenser/` | `/offerings/` |
| AI security pages (all languages) | `/offerings/` |
| Preventive cybersecurity pages (all languages) | `/offerings/product-security-engineering/` |
| Generative AI security tool pages (all languages) | `/offerings/product-security-engineering/` |
| GRC & compliance pages (all languages) | `/offerings/fractional-ciso/` |
| `/kontakt/`, `/en/contact/`, `/sv/kontakt/`, `/about/` | `/contact/` |

## Deploy

GitHub Pages builds and publishes the site automatically on every push to
`main`. The `CNAME` file points it at **scandinavian.dev**; keep it in the repo.

Workflow for changes:

1. Work on a branch (for example `redesign`).
2. Open a pull request into `main` and review it.
3. Merge. The live site updates within a minute or two.

GitHub Pages builds with its own Jekyll version (3.10) and only allows
whitelisted plugins. This site only uses whitelisted plugins
(`jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-redirect-from`) and builds the same
on Jekyll 3.10 and 4.4.

Under **Settings → Pages** in the repository, the source should be
"Deploy from a branch", branch `main`, folder `/ (root)`, with
"Enforce HTTPS" enabled.

## Project structure

```text
_config.yml              Site settings, Calendly, contact and legal details
_offerings/              One file per offering
_data/navigation.yml     Menu
_data/i18n/en.yml        Button and label text
_layouts/default.html    Page shell (head, header, footer)
_layouts/offering.html   Template for every offering page
_includes/               Header, footer, call-to-action banner, offerings overview, icons
_includes/illustrations/ Inline SVG illustrations
_includes/css/           CSS partials
assets/css/main.css      Joins the CSS partials into one file at build time
assets/js/main.js        Mobile menu (the site also works without JavaScript)
assets/images/           Hero image, logo, favicons, share thumbnail
index.html               Homepage
offerings.html           /offerings/
contact.html             /contact/ (About & Contact)
404.html                 Not-found page
robots.txt               Search engine rules + sitemap link
CNAME                    Custom domain for GitHub Pages
Dockerfile               Production-like build served by nginx
.devcontainer/           VS Code Dev Container setup
```
