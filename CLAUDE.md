# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static marketing website for Appostu (appostu.com), served via GitHub Pages. It's built on the **FlexStart Bootstrap template** (BootstrapMade) — plain HTML/CSS/JS, no build step, no package manager, no framework.

Pages are plain `.html` files at the repo root:
- `index.html` — main landing page (hero, about, values, stats, blog post, contact)
- `essential-oils-app.html` — landing page for a separate dōTERRA essential oils companion app
- `privacypolicy.html` — privacy policy
- `google618fe4c536414081.html` — Google Search Console verification file (do not remove/rename)
- `app-ads.txt`, `CNAME` — required at root for ad network (AdSense/AdMob) verification and custom domain routing respectively; keep them at the root

Each HTML page is self-contained: head, header/nav, main sections, footer, and script tags are duplicated per page rather than templated/shared. When editing shared elements (nav links, footer, contact info, analytics/AdSense tags), **update every HTML file individually** — there is no include/partial mechanism.

## Deployment

Deployed automatically by GitHub Actions (`.github/workflows/jekyll-gh-pages.yml`) on every push to `main`: Jekyll builds the site and publishes it to GitHub Pages. There is no local build command and nothing to run before pushing — pushing to `main` ships directly to production (appostu.com via CNAME). There are no tests or linters configured in this repo.

## Structure

- `assets/css/main.css` — site-wide custom CSS (the actual Sass sources are template-pro-only per `assets/scss/Readme.txt`, so this compiled CSS file is the only place to edit styles directly)
- `assets/js/main.js` — site-wide custom JS (nav toggle, scroll behavior, isotope/swiper init, etc.)
- `assets/vendor/` — third-party libraries used by the template: Bootstrap, Bootstrap Icons, AOS (scroll animations), GLightbox, Swiper, PureCounter, Isotope/imagesLoaded. Treat as vendored/read-only; don't hand-edit.
- `assets/img/` — all site imagery, organized by section (`blog/`, `clients/`, `portfolio/`, `team/`, `testimonials/`)
- `forms/contact.php`, `forms/newsletter.php` — PHP form handlers from the template. Per `forms/Readme.txt`, the working PHP/AJAX form library (`php-email-form.php`) is only available in the paid version of the template and is **not present** in this repo — these forms are non-functional as-is. GitHub Pages also cannot execute PHP, so any real form submission needs an external handler (e.g. Formspree) if implemented.

## Third-party integrations embedded directly in page `<head>`/`<body>`

- **Firebase** (`initializeApp`/`getAnalytics`, project `appostu-web`) — loaded via inline `<script type="module">` importing from `gstatic.com/firebasejs`
- **Google AdSense** (`adsbygoogle.js`, client `ca-pub-5574917194364525`) — validated by root `app-ads.txt`
- **Google Fonts** (Roboto, Poppins, Nunito) via `fonts.googleapis.com`

These are duplicated inline per page rather than centralized — when rotating keys/IDs or adding new tracking, grep across all root `.html` files rather than assuming one source of truth.

## Editing conventions

- Keep the FlexStart template's license/credit comment block in the footer (`Designed by BootstrapMade`) unless the pro license has been purchased — see the HTML comment in each footer.
- New pages should follow the existing pattern: copy the head boilerplate (fonts, vendor CSS, main CSS) and footer/vendor JS block from `index.html`, then add the nav link to that new page in the `<nav id="navmenu">` and footer "Useful Links" list of every other page.
