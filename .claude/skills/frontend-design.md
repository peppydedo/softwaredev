---
name: frontend-design
description: Project-specific frontend design guidance for DevCraft — a software development agency site targeting CTOs, founders, and engineering leads. Extends the upstream frontend-design skill with concrete token decisions, signature element, and tone guidance already decided for this project.
---

# Frontend Design — DevCraft Project

Extends the upstream `frontend-design` skill. Follow all principles there; the decisions below are already committed — don't revisit them unless the user asks.

## Subject & audience

DevCraft is a boutique software development agency. Audience: technical buyers (CTOs, founders, heads of engineering) who can smell generic. The page's single job: convert a curious visitor into an enquiry submission.

## Token system (already decided — use these exactly)

**Color**
- `--ink: #111318` — near-black with slight blue warmth (body text, headings on light)
- `--paper: #F8F7F4` — warm off-white (page background; avoids cold #F4F1EA cliché)
- `--amber: #C07C1A` — deep amber/gold (primary accent; deliberately avoids standard blue)
- `--amber-hover: #A56515` — darker amber for hover states
- `--charcoal: #1B2130` — dark blue-grey (hero, contact section backgrounds)
- `--surface: #FFFFFF` — card and form surfaces
- `--muted: #7A8296` — secondary text
- `--border: #E4E2DE` — warm dividers
- `--code-bg: #0D1117` — terminal/code panel background

**Why amber, not blue?** Blue is the default for dev agencies. Amber reads premium and boutique — signals craft and intentionality before the user reads a word.

**Typography**
- Display: `DM Serif Display` (italic) — hero H1 and section titles. Used with restraint.
- Body: `DM Sans` — everything else (300/400/500/600 weights)
- Monospace: `SF Mono`, `Fira Code` fallback — code panel only

**Pairing rationale:** DM Serif Display italic against DM Sans creates editorial contrast without serif-on-serif heaviness. The italic slant echoes the em-emphasis italic in H1 copy.

## Signature element

The hero's right panel is a live-looking code terminal (`src/api/users.ts`) with GitHub-style syntax highlighting. This is the page's single memorable thing — it shows craft before it claims it. Keep it on desktop only; hide on mobile. Do not replace it with an illustration or abstract shape.

## Layout principles for this project

- Hero: two-column on ≥900px (text left, terminal right), stacked on mobile
- Services: full-width grid with 1px border dividers between cards, amber top-border on hover
- Testimonials: editorial quotation mark (DM Serif Display italic `"`) in amber at 40% opacity
- Contact: dark `--charcoal` background section; form inputs use glass-dark styling
- Footer: `#0D1117`, flex row with copyright left and nav links right

## Copy tone

Speak to a technical buyer who is evaluating whether to trust you with their codebase. Be direct and specific. Avoid: "We're passionate about…", "innovative solutions", "leverage synergies". Prefer: concrete outcomes ("cut infrastructure costs by 40%"), active verbs ("ship", "build", "own"), and copy that sounds like a senior engineer wrote it.

## Do not

- Change the amber accent to blue/purple without explicit instruction
- Use emoji icons in service cards (use text tags instead)
- Add numbered step markers unless the content is actually a sequence
- Add animation beyond the cursor blink in the terminal and existing hover transitions
- Use a pure black (#000) or pure white (#fff) background
