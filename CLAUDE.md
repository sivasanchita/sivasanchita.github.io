# CLAUDE.md — Project rules for sivasanchita.github.io

This file tells Claude Code (and any future collaborator) how this project works.
Read it fully at the start of every session and follow it. If a request conflicts
with these rules, stop and ask Sanchita before doing anything.

---

## 1. What this project is

- Personal website for **Sanchita Sivaraman**, public health professional in Vancouver, BC.
- Purpose: a **virtual CV** (journey, work, skills, photos) and a **home for writing**
  (opinion pieces and reflections). Connected to her Substack, *Dear Sancho*.
- Audience: hiring managers, collaborators, community partners, and readers.
- Tone: warm, welcoming, reflective, curious, polished. Not flashy.
- Live site: https://sivasanchita.github.io (published from the `main` branch).

---

## 2. Workflow and safety rules (non-negotiable)

1. **Work only on the `dev` branch** (or a short-lived branch made from `dev`).
   Never edit `main` directly. `main` = the live site.
2. **Never commit, push, merge, rebase, or force-push** unless Sanchita explicitly asks
   in that session. Show changes and wait.
3. **Never delete files or folders** without listing them and getting a clear yes.
4. **Ask before installing anything** (gems, packages, tools). Explain what it is and why.
5. **Small, focused changes.** One section or feature at a time. Explain in plain language
   what changed and why.
6. **Commit messages** (when asked to commit): short, present tense, describe the change.
   Example: `Add footer with contact links`.
7. **Before any pull request to `main`**, run the checklist in section 9.
8. After each finished milestone, suggest a git tag (e.g. `v0.1-foundation`) as a
   restore point.

---

## 3. Privacy and content rules (this repo is PUBLIC, including its full history)

Deleting a file later does NOT remove it from history. So:

- **Never add**: phone numbers, home address, ID numbers, passwords, API keys, tokens,
  or any secret. If one ever appears in a file, stop and tell Sanchita immediately.
- **Only approved contact details**: email `sivasanchita@gmail.com`, LinkedIn, Substack, and
  Instagram `@your_travel_buddy_forever` (travel, on "Things I love" only).
- **No confidential or employer-owned material**: no internal documents, datasets,
  client, patient, or participant information. Only publicly available work and
  Sanchita's own assignments that she has confirmed are fine to share.
- **Other people**: don't name or show photos of other people unless Sanchita confirms
  they've agreed.
- **Photos**: strip location (GPS/EXIF) data before adding any image. Remind Sanchita
  of this whenever she adds photos.
- **No drafts in the repo.** Unfinished writing stays off GitHub until ready to publish.
- **Never invent biography facts.** Use obvious placeholders (e.g. `[About text here]`)
  until Sanchita supplies the real content.
- **No tracking or analytics** and no third-party embeds (widgets, pixels, comment systems)
  without discussing privacy trade-offs with Sanchita first.

---

## 4. Tech stack

- **Jekyll**, built by GitHub Pages. Use the `github-pages` gem in the `Gemfile` so local
  builds match what GitHub builds.
- Plugins (only GitHub Pages-supported ones): `jekyll-seo-tag`, `jekyll-sitemap`,
  `jekyll-feed`.
- Plain HTML, CSS, and minimal JavaScript. No frameworks, no build tools beyond Jekyll.
- **External resources**: only Google Fonts. No other CDNs or third-party scripts
  without approval.
- Local preview: `bundle exec jekyll serve`, then open http://localhost:4000.

### Required `.gitignore` entries
```
_site/
.jekyll-cache/
.jekyll-metadata
.sass-cache/
.bundle/
vendor/
.DS_Store
.env
*.log
```

---

## 5. Folder structure

```
/
├── CLAUDE.md             ← this file
├── README.md             ← short human-facing description of the project
├── _config.yml           ← site settings (title, description, URL, plugins)
├── Gemfile               ← github-pages gem
├── .gitignore
├── index.html            ← home / About
├── 404.html              ← friendly not-found page
├── _layouts/             ← default.html, page.html, post.html
├── _includes/            ← header.html, footer.html, head.html
├── _data/love.yml        ← travel photos and books for "Things I love"
├── _posts/               ← published writing (YYYY-MM-DD-title.md)
├── pages/                ← journey, work, opinions, skills, things-i-love
└── assets/
    ├── css/style.css
    ├── images/           ← compressed, EXIF-stripped images only
    └── favicon/
```

---

## 6. Design system

All colours live as CSS variables in ONE place (top of `assets/css/style.css`).
Never hard-code colours elsewhere.

| Variable              | Value     | Use                                               |
|-----------------------|-----------|---------------------------------------------------|
| `--bg-page`           | `#F7F1E6` | Page background (warm paper)                      |
| `--bg-card`           | `#EFE5D4` | Tinted bands, chips, highlighted sections (sand)  |
| `--bg-dark`           | `#173E46` | Footer and dark bands (deep teal)                 |
| `--bg-frame`          | `#FFFDF8` | White mat around framed photos                    |
| `--color-primary`     | `#1B5E6B` | Headings, links, buttons (teal)                   |
| `--color-accent`      | `#E8914A` | Lines, underlines, small details ONLY (apricot)   |
| `--color-accent-text` | `#9A4A16` | Apricot for text on light backgrounds             |
| `--color-text`        | `#1E2A2E` | Body text (ink)                                   |
| `--color-muted`       | `#52636A` | Meta lines, captions, secondary text              |

- **Fonts**: Lora (headings), Source Sans 3 (body). `font-display: swap`.
- **Body text**: 18px, line-height ~1.7, max line length ~70 characters.
- **Header**: name, line "Curiosity · Evidence · Impact", numbered nav
  (01 About, 02 Journey, 03 Work & impact, 04 Opinions, 05 Skills, 06 Things I love).
- **Footer**: dark band with name and tagline, "Vancouver, BC", LinkedIn, Substack,
  "Get in touch" (mailto).
- **Style**: calm, lots of space, no gradients, glitter, or heavy animation.
  Subtle hover effects only.

### Editorial / magazine style (the look of every section page)

The site reads like a printed magazine or newspaper feature. When adding or changing
a page, keep to these patterns (all styles already exist in `style.css`):

- **Masthead header**: name and small-caps tagline on the left, "Get in touch ↗" on
  the right, and the numbered nav running full width between two hairline rules.
- **Page opening** (handled by `_layouts/page.html` from front matter):
  small ornament (rule ✦ rule) → eyebrow `05 / Skills` → big two-line serif headline
  (`headline: ["Line one", "line two."]`) → one muted lead sentence (`lead:`).
  Optional framed photo beside the headline with `intro_photo:` (see Things I love).
- **Rules, not boxes**: separate things with thin hairline rules and white space.
  No filled cards or rounded coloured boxes. A full-width tinted band (`.band`)
  can alternate with plain sections to give rhythm.
- **Stats row** (`.stats.stats-row`): big serif numbers divided by vertical rules,
  followed by "jump to" links (`.jump-links`) where a page is long.
- **Journey is a single timeline** (`.timeline`): date, role, organization, short
  text, then that period's posts and photos. Sanchita prefers how it flows over
  a chapter layout.
- **Chapters** (`.chapter`, available but not currently used): eyebrow + heading + one-line blurb in
  a sticky left column; entries on the right, each with a muted meta line
  (organization · place · dates), serif title, short paragraph, and an apricot
  keyword line (`.tag-line`), then posts and photos.
- **Numbered grid** (`.num-grid`, used on Skills): two columns, apricot serif
  number, heading, short text, a rule, keyword line, then "in practice" links.
- **Captions are optional.** Don't add a caption just to fill space.
- **Photos are framed prints** (`.frame`, `.gallery-item`): white mat, soft
  shadow, square corners. A slight tilt (`.frame-tilt`) only for one hero photo.
- **Section intros** (`.section-intro`): small-caps eyebrow, sentence-case serif
  heading ending in a full stop ("On my bookshelf."), one muted sentence.
- **Every section page ends** with "Continue exploring → next page" (automatic).
- Headlines, eyebrows and blurbs are written from Sanchita's own content —
  never invent facts to fill a layout.

### Things I love content

Travel photos and books are listed in `_data/love.yml`; the page fills itself in.
Books without a cover image get a printed-style cover in the site colours.
Empty lists show "coming soon".

---

## 7. Accessibility (WCAG 2.1 AA)

- Text contrast at least 4.5:1 (3:1 for large text). Never use `--color-accent`
  for body text.
- Semantic HTML: one `<h1>` per page, headings in order, `<nav>`, `<main>`, `<footer>`.
- `<html lang="en-CA">`.
- "Skip to content" link at the top of every page.
- Every image has meaningful `alt` text (or `alt=""` if purely decorative).
- Everything works by keyboard; visible focus styles.
- Respect `prefers-reduced-motion`.
- Mobile-first and responsive; navigation collapses into an accessible menu.

---

## 8. Performance, SEO, and sharing

- Images: compress, prefer WebP, set `width`/`height`, use `loading="lazy"`
  below the fold. Aim for under ~300 KB per image.
- `jekyll-seo-tag` in `<head>` for titles, descriptions, and Open Graph previews.
- Every page has a unique `title` and `description` in its front matter.
- `jekyll-sitemap` for search engines; `jekyll-feed` for the writing RSS feed.
- Favicon and a default social-share image.
- External links: `target="_blank" rel="noopener noreferrer"`.

---

## 9. Pre-publish checklist (before any pull request to `main`)

- [ ] `bundle exec jekyll build` runs with no errors or warnings.
- [ ] Previewed locally on desktop AND a narrow mobile width.
- [ ] All links work (no broken internal links, correct external URLs).
- [ ] No placeholders left on pages being published (or intentionally marked "coming soon").
- [ ] No private information, secrets, or unapproved content (section 3).
- [ ] Images compressed, EXIF stripped, alt text present.
- [ ] Spelling checked (Canadian English).
- [ ] Contrast and keyboard navigation checked.

---

## 10. Writing posts

- File: `_posts/YYYY-MM-DD-short-title.md`
- Front matter template:
```yaml
---
layout: post
title: "Post title"
description: "One-sentence summary for previews and search."
date: YYYY-MM-DD
category: reflection   # or: opinion
tags: []
substack_url:          # optional: link if also published on Dear Sancho
---
```
- Canadian spelling. Sentence case headings.
- Claude may help edit or format, but must not change Sanchita's meaning or voice
  without asking.

---

## 11. Decision log

Record significant decisions here (date — decision — reason).

- 2026-09-24 — Jekyll on GitHub Pages — native to Pages, Markdown posts, no paid hosting.
- 2026-09-24 — `dev` branch for work, `main` protected by ruleset — nothing goes live by accident.
- 2026-09-24 — Palette: teal + apricot on sage mist / soft sand — warm, welcoming, readable.
- 2026-09-24 — Commits use GitHub no-reply email — keeps personal email out of history.
- 2026-09-24 — Header line "Curiosity · Evidence · Impact" — chosen by Sanchita over "Evaluation · Reflection · Community".
- 2026-09-24 — Home page is the About page (nav 01 links to `/`) — matches folder structure; other pages live in `pages/`.
- 2026-09-24 — Brand direction: health systems thinking and analysis — where Sanchita's career is headed; home headline is Peter Senge's systems-thinking quote (*The Fifth Discipline*). Avoid quotes that undersell her or could read as about her body.
- 2026-09-24 — "Writing" renamed "Learnings" (`/learnings/`) — Sanchita's choice; posts live under `/learnings/`.
- 2026-09-24 — Instagram `@your_travel_buddy_forever` approved for the travel section — Sanchita confirmed.
- 2026-09-24 — Organization badges (initials in site colours) instead of real logos — logos are trademarks and can imply endorsement; badges stay on-brand.
- 2026-09-24 — Photos with other people are cropped to Sanchita only (e.g. graduation photo) unless those people have agreed.
- 2026-09-24 — "Learnings" renamed "Opinions" (`/opinions/`) — Sanchita's choice.
- 2026-09-24 — Real organization logos on Journey, at Sanchita's request — saved in `assets/images/logos/` (never hotlinked), shown on white tiles; organization names link to their websites.
- 2026-09-24 — Anyone other than Sanchita in a photo gets their face fully pixelated and blurred (patients, community members, event attendees). Photos of children in clinical settings are left out unless a guardian has consented.
- 2026-09-24 — Exception: event photos already posted publicly (e.g. CESBC 2024 on LinkedIn) where other people are incidental audience can be used unblurred — Sanchita's decision. Patients and community members are still always blurred.
- 2026-09-24 — Logos removed from Journey (too small to read beside the timeline); organization names link to their websites instead. Design direction: visual first — photos and posts lead, text stays crisp.
- 2026-09-24 — No employer-sensitive detail on the site (funding amounts, funder names for internal projects, land use work, national adoption claims) — fine on the CV, not on a public page. Home page stays professional: no theory sections or framework diagrams.
- 2026-09-24 — Home headline changed to Martin Luther King Jr.'s "inescapable network of mutuality" (Letter from Birmingham Jail, 1963), replacing Senge — Sanchita's choice.
- 2026-09-24 — Headline changed to Audre Lorde, "There is no such thing as a single-issue struggle…" ("Learning from the 60s", 1982). About section rebuilt from the first draft: access to care, resilient communities, 4+ years, listening-first and relationship-based approach.
- 2026-09-24 — No "Dr." title or post-nominals (BDS, MPH) in the header or hero — Sanchita's final choice. Hero reads "Hi, I'm Sanchita."
- 2026-09-24 — Editorial / magazine redesign (Sanchita's request, inspired by the layout of a peer's site; no content or images copied): warm paper background, masthead header, big two-line serif headlines, hairline rules instead of filled cards, framed photos, dark footer, "Continue exploring" links. Journey became three chapters; Skills a numbered grid; Things I love reads from `_data/love.yml`. Palette table updated (sage mist background replaced by warm paper; teal and apricot kept).
- 2026-09-24 — Journey reverted to the single timeline (restyled to match), chapters dropped — Sanchita: the timeline flowed better. Things I love hero photo is the rainy beach umbrella photo, no caption.
