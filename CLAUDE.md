# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the project

No build step. Open `index.html` directly in a browser:

```
start index.html          # Windows
open index.html           # macOS
```

## Architecture

Single-file static site — `index.html` contains everything:

- **`<style>` block** — all CSS, structured as:
  - CSS custom properties on `:root` (color palette, shadow tokens, radius)
  - Reset & base styles
  - Component sections in page order: Navbar → Hero → Services → Testimonials → Contact Form → Footer
  - Responsive breakpoints at `640px`, `768px`, and `1024px` (mobile-first)

- **HTML body** — semantic sections in order: `<header>` (navbar) → `<main>` → `<footer>`, with `id` anchors `#home`, `#services`, `#testimonials`, `#contact`

- **`<script>` block** (bottom of body) — vanilla JS for:
  - Navbar scroll class (`.scrolled`) via `window.addEventListener('scroll', ...)`
  - Hamburger toggle (`#nav-toggle` / `#main-nav`) with `aria-expanded` and Escape-to-close
  - Smooth-scroll fallback for `a[href^="#"]` anchors
  - Form validation and submission on `#enquiry-form`

## Design tokens

All colours and shadows are CSS variables defined on `:root`. Edit these to retheme the whole page:

| Variable | Purpose |
|---|---|
| `--color-primary` | Dark hero/navbar background |
| `--color-accent` | Buttons, highlights, avatar fills |
| `--color-accent-h` | Button hover state |
| `--color-surface` | Page and card backgrounds |
| `--color-text` / `--color-muted` | Body copy |

## Form submission

The form (`#enquiry-form`) currently logs collected data to `console.log`. A commented-out `fetch()` block is present at the bottom of the submit handler — uncomment and point at a real endpoint to wire up a backend.

Validation rules: Name required, Email required + regex, Message required. Phone and Service are optional/pre-selected.
