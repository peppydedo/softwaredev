# DevCraft — Software Company Landing Page

A modern, responsive single-page marketing website for a custom software development agency. Built with plain HTML, CSS, and vanilla JavaScript — no frameworks, no build step.

## Live Site

[peppydedo.github.io/softwaredev](https://peppydedo.github.io/softwaredev/)

## Features

- **Sticky navbar** with smooth-scroll anchor links and a mobile hamburger menu
- **Hero section** with gradient background, headline, stats, and CTA buttons
- **Services grid** — responsive 1→2→4 column layout (Web Apps, Mobile, APIs, Cloud & DevOps)
- **Testimonials** — 3 cards with hover lift effect
- **Enquiry form** — client-side validation, inline error messages, success confirmation, and a console-logged payload (with a commented-out `fetch()` stub for wiring up a real backend)
- Fully responsive via CSS Grid and Flexbox (breakpoints at 640px, 768px, 1024px)
- Accessible: semantic HTML5, labelled inputs, `role="alert"` error spans, `aria-expanded` on the nav toggle

### SEO

- Optimised `<title>` tag with primary keywords leading
- `<meta name="description">` with target keywords
- `<link rel="canonical">` pointing to the live URL
- Open Graph (`og:title`, `og:description`, `og:url`, `og:type`) for rich social previews
- Twitter Card tags
- JSON-LD structured data — `Organization` (name, address, phone, email, aggregate rating) + `WebSite`
- Inline SVG favicon and `theme-color` meta
- `robots.txt` and `sitemap.xml`

## Running locally

Open `index.html` directly in a browser — no server or build step needed:

```bash
# Windows
start index.html

# macOS / Linux
open index.html
```

## Deployment

Deployed automatically to GitHub Pages via GitHub Actions on every push to `main`. See [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml).

> **Note:** if you point a custom domain at this site, update the `canonical`, Open Graph URLs, JSON-LD `@id`/`url` fields, and `sitemap.xml` to match the new domain.
