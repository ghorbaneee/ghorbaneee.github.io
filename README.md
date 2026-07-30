# ghorbaneee.github.io

Personal academic website for Amirhossein Ghorbani, built with **Jekyll** and hosted on **GitHub Pages**.

## Why Jekyll

GitHub Pages builds Jekyll sites natively — push to `main` and the live site
updates in 1–2 minutes, no CI workflow required. It also has first-class
support for **data files** (`_data/*.yml`), which this site leans on heavily:
every publication, award, course, and news item lives in a small YAML file
instead of being hand-coded into HTML. That means updating the site after a
new paper or award almost never means touching a template.

## Repository structure

```
├── _config.yml          # Site title, nav links, social URLs, author info
├── Gemfile               # Matches the gem versions GitHub Pages builds with
│
├── _data/                # <-- You'll edit these files most often
│   ├── publications.yml  # Journal articles + conference papers
│   ├── education.yml     # Degrees, shown on Home > About
│   ├── experience.yml    # Short career timeline, shown on Home > About
│   ├── teaching.yml      # Full TA course list, shown on /teaching/
│   ├── awards.yml        # Honors & awards, shown on Home + /cv/
│   ├── courses.yml       # Certificates / professional development, /cv/
│   ├── news.yml          # News & Updates timeline, shown on Home
│   ├── projects.yml      # Project cards, shown on Home
│   ├── research_pillars.yml  # The 3-4 featured research areas, Home
│   ├── research_tags.yml     # Secondary interest tags, Home
│   └── skills.yml        # Software + languages, shown on /cv/
│
├── _layouts/
│   ├── default.html      # Base HTML shell (head, header, footer, scripts)
│   ├── home.html         # Wraps default.html, flags page.layout == "home"
│   └── page.html         # Adds a page title/subtitle header, used by inner pages
│
├── _includes/
│   ├── head.html         # <head> meta tags, fonts, SEO tag, JSON-LD
│   ├── header.html       # Top nav + the Home page's in-page sub-nav
│   ├── footer.html       # Site footer
│   ├── social-links.html # The row of email/Scholar/GitHub/LinkedIn icons
│   └── icon.html         # All inline SVG icons in one place
│
├── assets/
│   ├── css/style.css     # The entire stylesheet (no framework, no build step)
│   ├── js/main.js        # ~15 lines: mobile nav toggle only
│   ├── img/              # profile.jpg, favicons
│   └── cv/               # Amirhossein_Ghorbani_CV.pdf (downloadable + embedded)
│
├── index.html             # Home: hero, About, Research, Projects, News, Awards
├── publications.html       # /publications/
├── teaching.html            # /teaching/
├── cv.html                  # /cv/
├── contact.html              # /contact/
└── 404.html
```

## How to update the site

**Add a publication** → open `_data/publications.yml`, add an entry at the
top of `journal_articles:` or `conference_papers:`. No HTML editing needed.

**Add a news item** → add a line to the top of `_data/news.yml`.

**Add an award** → add an entry to the top of `_data/awards.yml`.

**Add a teaching term** → add a course under the right institution in
`_data/teaching.yml`.

**Update your photo or CV** → replace `assets/img/profile.jpg` or
`assets/cv/Amirhossein_Ghorbani_CV.pdf` with a new file of the *same name*
(no code changes needed), or update the filename in `_config.yml` /
`cv.html` if you rename it.

**Change contact info, social links, or nav** → edit `_config.yml`.

After any change, commit and push to `main` — GitHub Pages rebuilds
automatically within a minute or two.

## Local preview (optional, requires Ruby + Bundler)

```bash
bundle install
bundle exec jekyll serve
# open http://localhost:4000
```

## Deploying / updating on GitHub

1. Clone your existing repo (or if you already have it locally, `cd` into it):
   ```bash
   git clone https://github.com/ghorbaneee/ghorbaneee.github.io.git
   cd ghorbaneee.github.io
   ```
2. Delete the old placeholder files and copy in everything from this folder.
3. Commit and push:
   ```bash
   git add .
   git commit -m "Rebuild site: Jekyll academic portfolio"
   git push origin main
   ```
4. In the repo's **Settings → Pages**, make sure the source is set to
   "Deploy from a branch" → `main` → `/ (root)`. Since the repo is named
   `ghorbaneee.github.io`, GitHub Pages is enabled by default.
5. Your site will be live at **https://ghorbaneee.github.io** within a few
   minutes. Check the **Actions** tab if the build fails — it will show the
   exact Jekyll error.

## Design notes

- **Palette**: warm ivory background (`#FAF7F1`), sage-green primary accent,
  terracotta secondary accent — a "soft academic pastel" look distinct from
  the stark black-and-white of many faculty pages, while still reading as
  serious and minimal.
- **Type**: Source Serif 4 for headings (academic, editorial feel), Inter
  for body text (fast-loading, highly legible at small sizes).
- **No JS framework, no CSS framework, no build step required to view the
  site** — just Jekyll + plain CSS + ~15 lines of vanilla JS for the mobile
  menu. This keeps the site fast and easy to maintain long-term.
- **Navigation** is intentionally short (Home, Publications, Teaching, CV,
  Contact). About, Research, Projects, News, and Awards live as sections
  on the Home page with in-page anchor links, since each section is only a
  few paragraphs — a full page per section would be mostly empty space.
  Publications and Teaching get their own pages because those lists will
  keep growing.
- **SEO**: `jekyll-seo-tag` handles title/meta/Open Graph tags automatically
  from `_config.yml`; a `Person` JSON-LD block in `head.html` gives Google
  structured data for you as a researcher; `jekyll-sitemap` auto-generates
  `sitemap.xml`; `robots.txt` points crawlers to it.
- **Accessibility**: skip-to-content link, visible focus states, semantic
  landmarks (`header`/`nav`/`main`/`footer`), alt text on the profile photo,
  `aria-current`/`aria-label` on nav and social icons, reduced-motion support.

## Ideas for later

- **Gallery page** — once you have conference/lab photos, add a `gallery.html`
  page and a matching nav entry; the CSS `.card-grid` class already works
  well for a photo grid.
- **ORCID** — add your ORCID URL to `site.social.orcid` in `_config.yml` and
  the icon will appear automatically in the footer/contact links.
- **Google Analytics / Plausible** — add the tracking snippet to
  `_includes/head.html` if you want visitor stats.
- **Contact form** — GitHub Pages has no backend, so the Contact page uses a
  plain `mailto:` link. If you want a real form, Formspree or Getform can be
  wired in with a couple of `<input>` fields and no server code.
