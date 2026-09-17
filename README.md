# Handoff: Gowrish Kumar Reddy — Research Portfolio Site

## Overview

A six-page personal research portfolio for **Gowrish Kumar Reddy**, a prefinal-year B.Tech CSE (AI/ML) student at SRM Ramapuram working on mechanistic interpretability, AI alignment & safety, and vision models. The site is academic-facing: its audience is researchers, lab leads, and PhD/MATS admissions readers. It is content-first, text-only (no photography, no charts), and deliberately quiet.

Pages: **Home · Research · About · CV · Notes · Contact**

## About the Design Files

The files in `design_files/` are **design references created in HTML** — prototypes showing the intended look, copy, and structure. They are **not production code to copy directly**.

They are authored in a proprietary "Design Component" format (`.dc.html` files paired with `support.js`), which renders them in the design tool. Do not attempt to port that runtime. Open each file in a browser to see the rendered design, and read the markup for exact values.

**The task is to recreate these designs in a real codebase.** For a static personal site the natural choices are Astro, Next.js (static export), Eleventy, or plain HTML + CSS — any of these suits it, since there is no interactive state beyond navigation. Pick one and implement using its conventions. If the developer already has a site scaffold, use its existing patterns and component library instead.

Two practical notes for a real deployment:
- The design files link between pages as `Home.dc.html`, `Research.dc.html`, etc. In production these should be clean routes: `/`, `/research`, `/about`, `/cv`, `/notes`, `/contact`.
- The CV page has a deliberately non-functional "PDF coming soon" button. When the owner supplies `cv.pdf`, it becomes a real download link.

## Fidelity

**High-fidelity.** Colors, typography, spacing, and copy are final and should be reproduced faithfully. Every value in this document is taken from the design files. The copy in particular is the owner's own voice and was iterated on — **do not rewrite it.**

The design is **fluid, not fixed-width**. It must reflow down to mobile widths. No fixed heights on text containers.

---

## Design Tokens

### Colors

| Token | Value | Use |
|---|---|---|
| Paper | `#f9f5ec` | Page background |
| Rule line | `rgba(120,100,60,.07)` | Ruled-paper horizontal lines |
| Ink | `#332e24` | Primary body text |
| Ink 80% | `rgba(51,46,36,.8)` | Secondary body text |
| Ink 78% | `rgba(51,46,36,.78)` | Metadata, footer links, captions |
| Ink 72% | `rgba(51,46,36,.72)` | Long-form paragraph body, dates |
| Ink 70% | `rgba(51,46,36,.7)` | Uppercase section eyebrows |
| Ink 68% | `rgba(51,46,36,.68)` | Lowest-emphasis text |
| Heading brown | `#4a3d19` | Large handwritten page headings |
| Accent brown | `#5a4a1f` | Handwritten subheadings, links |
| Link hover | `#8a6f1f` | `a:hover` |
| Sticky yellow | `#fef4a8` | Sticky-note backgrounds |
| Sticky ink | `#5a5320` | Text on sticky notes |
| Panel wash | `rgba(90,74,31,.06)` | Quote panels, contact cards |
| Chip background | `rgba(90,74,31,.13)` – `.14` | Tag/status chips |
| Dashed rule | `rgba(51,46,36,.28)` | Section dividers, dashed button borders |

**Accessibility note:** the ink opacities above were raised from an earlier draft specifically to clear **4.5:1 contrast** against the cream ground at small sizes. Do not lower them. If you re-theme, re-check contrast rather than reusing alpha values.

### Ruled-paper background

Applied to the page wrapper on every page:

```css
background: #f9f5ec;
background-image: repeating-linear-gradient(
  #f9f5ec 0 33px,
  rgba(120,100,60,.07) 33px 34px
);
```

### Typography

Three Google Fonts:

| Family | Weights | Role |
|---|---|---|
| **Caveat** | 500, 600 | Handwritten: wordmark, page headings, section subheadings, footer line |
| **Newsreader** | 400, 500, 600 + italic | Serif: lead paragraphs, project titles, emphasis |
| **Work Sans** | 400, 500, 600 | Sans: nav, body copy, metadata, chips, lists |

```
https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;0,6..72,600;1,6..72,400&family=Work+Sans:wght@400;500;600&family=Caveat:wght@500;600&display=swap
```

Type scale as used:

| Element | Family | Size | Weight | Line-height | Other |
|---|---|---|---|---|---|
| Wordmark ("Gowrish") | Caveat | 24px | 600 | — | color `#5a4a1f` |
| Nav links | Work Sans | 13px | 400 | — | lowercase |
| Home h1 | Caveat | `clamp(40px,6.4vw,64px)` | 600 | 1.02 | color `#4a3d19` |
| Inner-page h1 | Caveat | `clamp(36px,5.4vw,52px)` | 600 | 1.05 | color `#4a3d19` |
| Section subheading | Caveat | 27–28px | 600 | — | color `#5a4a1f` |
| Lead paragraph | Newsreader | 19–20px | 400 | 1.6–1.62 | `text-wrap: pretty` |
| Project title (Home) | Newsreader | 22px | 400 | 1.3 | — |
| Project title (Research h2) | Newsreader | 27px | 500 | 1.25 | — |
| Project title (CV) | Newsreader | 19px | 400 | — | — |
| Body paragraph | Work Sans | 15–15.5px | 400 | 1.72–1.74 | `text-wrap: pretty` |
| Project body | Work Sans | 14.5px | 400 | 1.65–1.68 | max-width 62ch |
| Metadata row | Work Sans | 12.5px | 400 | — | — |
| Chip / tag | Work Sans | 12–13px | 400 | — | — |
| Eyebrow (uppercase) | Work Sans | 11.5px | 400 | — | `letter-spacing:.12–.14em`, `text-transform:uppercase` |
| Pull quote (Home) | Newsreader italic | 20px | 400 | 1.45 | color `#4a3d19` |
| Pull quote (About) | Newsreader italic | 22px | 400 | 1.4 | color `#4a3d19` |

Measure caps: lead paragraphs `52–56ch`, body `60–62ch`. Keep them.

### Layout & spacing

- Content column: `max-width: 780px; margin: 0 auto; padding: 0 34px`.
- Every page is a vertical stack of these blocks; vertical rhythm comes from each block's `padding-top`: `30px` (nav), `52–56px` (hero), `36–66px` (subsequent sections), `52px` (footer). Page wrapper has `padding-bottom: 84px`.
- Section dividers: `border-top: 1.5px dashed rgba(51,46,36,.28)` with `padding-top: 24–30px` on the inner container.
- Use flex/grid with `gap` for all sibling groups (nav, footer links, chip rows, card grids). Never rely on inline whitespace.

### Other values

- Border radius: `2px` (buttons), `3px` (panels, chips, cards). Nothing more rounded.
- Sticky notes: `transform: rotate(-1.2deg)` (badge) or `rotate(-.7deg)` (notes), `box-shadow: 0 1px 3px rgba(0,0,0,.12)`, padding `6px 12px` (badge) / `16px 18px` (note).
- Dashed button: `border: 1.5px dashed #332e24; border-radius: 2px; padding: 10px 20px; font-size: 13.5px`.
- Underlined text link: `text-decoration: underline; text-underline-offset: 2–3px`.
- Chips: `padding: 5px 11px` (small) / `7px 14px` (large), `border-radius: 3px`.

---

## Shared Components

### Header / nav

Present identically on all six pages. Flex row, `justify-content: space-between`, `align-items: baseline`, `flex-wrap: wrap`, `gap: 14px`.

- **Left:** wordmark "Gowrish" — Caveat 24px/600, `#5a4a1f`, links to Home.
- **Right:** six lowercase links in a flex row, `gap: 20px`, 13px, `rgba(51,46,36,.78)`: `home · research · about · cv · notes · contact`.
- **Current page:** `color: #332e24` and `border-bottom: 1.5px solid #5a4a1f`.
- No sticky positioning, no mobile hamburger — it wraps naturally.

### Footer

On Home, Research, About, CV, Notes (Contact has its own ending — see below).

- Caveat 26px, `#5a4a1f`: **"say hi — I'd like that."**
- Below it, a flex row, `gap: 18px`, 13px: **Email** (`mailto:gowrishkumar61@gmail.com`), **GitHub**, **Twitter**, **LinkedIn**.
- Labels only — never render the raw email address or handle in the footer. This was an explicit request.

### Links

```css
a { color: #5a4a1f; text-decoration: none; }
a:hover { color: #8a6f1f; }
```

Define these globally even where no links exist yet.

---

## Screens

### 1. Home (`/`)

**Purpose:** establish who he is and what he works on in under a screen, then send readers to Research.

Deliberately short. Do not add sections.

**Layout, top to bottom:**

1. **Nav** (shared).
2. **Hero** (`padding-top: 56px`):
   - Sticky badge, rotated `-1.2deg`: "prefinal-year · SRM Ramapuram · interpretability & AI safety"
   - `h1`, Caveat: **"Hi, I'm Gowrish."**
   - Lead paragraph, Newsreader 20px, max-width 52ch: *"I work on mechanistic interpretability and AI alignment & safety — mostly by taking small models apart until I understand what each piece is doing. I'm a B.Tech CSE (AI/ML) student, and this is where I keep track of the work."*
   - **Quote panel** (`rgba(90,74,31,.06)`, radius 3px, padding `20px 24px`, max-width 52ch):
     - Newsreader italic 20px, `#4a3d19`: *"You cannot control something you don't understand."*
     - Caption, 12.5px: *"From an anime film — and honestly, it's why I'm here. We're building systems more capable than our ability to explain their internals. Interpretability is the one field that confronts that gap head-on."*
     - The attribution is intentionally **"an anime film"** — unnamed. Keep it that way.
   - Two CTAs in a flex row, `gap: 14px`: dashed button "see what I've been working on →" (→ Research) and an underlined link "read my CV" (→ CV).
3. **Work section** (`padding-top: 66px`):
   - Caveat 27px subheading: "what I've been working on"
   - Two entries separated by `1.5px dashed` rules (first has `border-top`, second has both `border-top` and `border-bottom`), each `padding: 22px 0`:
     - **"Mechanistic interpretability pipeline for GPT-2 Small"** — body paragraph, then metadata row: `2026 · findings doc + 14 figures · GitHub ↗` linking to `https://github.com/gowrish-kumar-61/mechanistic-interp-gpt2`
     - **"Benchmarking sub-3B VLMs on CPU-only hardware"** — body paragraph, then metadata row: `2026 ·` + chip "in progress · not public". **No link** — the repo is private.
   - Sticky note, rotated `-.7deg`, max-width 44ch: "**Right now:** rebuilding math foundations from zero, then ARENA 3.0 properly. *the full plan →*" (links to Research)
4. **Footer** (shared).

**Optional flags** (the design file exposes these as toggles; implement as props/config if useful, otherwise hard-code both on):
- `showQuote` (default true) — the hero quote panel
- `showWorkingOn` (default true) — the "Right now" sticky note

### 2. Research (`/research`)

**Purpose:** the substantive page. Both projects in full, plus what's next.

1. **Nav.**
2. **Hero:** h1 "Research" + lead paragraph, max-width 54ch: *"Two things I'm working on. One is about understanding what a model has learned; the other is about what happens when you try to actually run one."*
3. **Project 01** (dashed `border-top`, `padding-top: 26px`):
   - Header row, `space-between`, wrapping: eyebrow "01 · Mechanistic interpretability" | date "2026"
   - `h2` Newsreader 27px/500: "A mechanistic interpretability pipeline for GPT-2 Small, built from scratch"
   - Newsreader 17px paragraph (the "why from scratch" rationale), then Work Sans 15px paragraph with the results. **`<b>` on the two findings:** "Previous Token Head at L3H0" and "Induction Head at L5H1".
   - Chip row, `gap: 10px`: `raw PyTorch` · `SVD weight analysis` · `activation patching` · `14 figures`
   - Dashed button: "read the findings doc & figures on GitHub ↗"
4. **Project 02** (same structure):
   - Eyebrow "02 · Vision models & systems" | date "2026 · in progress"
   - `h2` "Empirical benchmarking of sub-3B VLMs on CPU-only hardware"
   - Two paragraphs; **`<b>`** on "Moondream2 takes 700+ seconds per image on Intel CPUs".
   - Chips: `SmolVLM` · `Moondream2` · `TinyLLaVA` · `VQAv2`
   - Italic 12.5px note: "Repository isn't public yet — happy to talk about the results in the meantime."
5. **"what's coming"** (Caveat 28px) — panel `rgba(90,74,31,.06)`, radius 3px, padding `22px 24px`, max-width 60ch. Two paragraphs: math foundations (3Blue1Brown, Boyd's *VMLS* — `<i>` on VMLS), then ARENA 3.0 → paper replication → MATS 2027.
6. **Footer.**

### 3. About (`/about`)

1. **Nav.**
2. **Hero:** h1 "About me", Newsreader 19px lead paragraph (who he is, what he works on), then Work Sans 15.5px paragraph ("Most of my time goes into small, self-contained experiments…").
3. **"how I got here"** (Caveat 28px):
   - Quote panel, max-width 56ch: Newsreader italic 22px *"You cannot control something you don't understand."* with a 12.5px attribution line **"— from an anime film"**.
   - Three paragraphs: the accidental hook, the capability/explanation gap, and the reframing. This is the most personal copy on the site — reproduce verbatim.
4. **"what I'm interested in"** (Caveat 28px): three-column grid, `repeat(auto-fit, minmax(min(100%,220px), 1fr))`, `gap: 20px`. Each cell is a Newsreader 18px label + 14px description. Order matters — **Mechanistic interpretability**, then **AI alignment & safety**, then **Vision models**.
5. **Education row:** dashed `border-top`, flex `space-between` baseline, wrapping. Left: Newsreader 19px "B.Tech, Computer Science & Engineering (AI/ML)" + 14px "SRM Institute of Science & Technology, Ramapuram". Right: 13px "2024 — 2028".
6. **Footer.**

**No photo and no skills/tools section** — both were explicitly removed. Don't reintroduce them.

### 4. CV (`/cv`)

Structured, scannable, closest to a document. **No GPA anywhere** — an explicit decision.

1. **Nav.**
2. **Header:** flex row, `align-items: flex-end`, wrapping — h1 "Curriculum vitae" on the left; on the right a **disabled-looking** "PDF coming soon" chip (`1.5px dashed rgba(51,46,36,.35)`, radius 2px, `padding: 9px 16px`, `rgba(51,46,36,.72)`, `cursor: default`, not a link). Below: "Gowrish Kumar Reddy · Email · GitHub" with the two underlined links.
3. **Education** (eyebrow): the degree row as on About.
4. **Research & projects** (eyebrow): two entries, each a title/date row then a `<ul>` (`padding-left: 18px`, 14.5px, `line-height: 1.7`, max-width 62ch).
   - GPT-2 Small — **2026** — five bullets: raw-PyTorch pipeline; Previous Token Head L3H0 at 0.87 (19× baseline); Induction Head L5H1 via activation patching; SVD-predicted then experimentally verified; findings report with 14 figures + GitHub link.
   - CPU VLM benchmarking — **2026 · ongoing** — three bullets: the three models on VQAv2; the GPU-assumption gap; the Moondream2 700+ s/image result.
5. **Technical skills** (eyebrow): grid `repeat(auto-fit, minmax(min(100%,240px), 1fr))`, `gap: 16px 28px`, four cells, each a muted category label above the values:
   - Languages — Python
   - ML & interpretability — PyTorch, Hugging Face, TransformerLens
   - Scientific computing — NumPy, Pandas, Matplotlib
   - Tooling — Git, LaTeX
6. **Current focus** (eyebrow): one paragraph, max-width 62ch, ending in a link to Research.
7. **Footer.**

**When the real CV PDF arrives:** replace the "PDF coming soon" `<span>` with an `<a href="/cv.pdf" download>` styled as the dashed button, and align the page content to the PDF.

### 5. Notes (`/notes`)

An intentional empty state — honest and dry. It should not look broken or unfinished.

1. **Nav.**
2. **Hero:** h1 "Notes" + Newsreader 19px line: *"Nothing here yet — by design."*
3. **Body:** dashed `border-top`, max-width 60ch, two 15.5px paragraphs explaining the choice (an empty page over a padded one; the work is going into research and foundations). Second paragraph ends with a link to the research page.
4. **Footer.**

When this becomes a real blog, the empty-state copy is replaced by a post list; keep the same header/measure.

### 6. Contact (`/contact`)

The one page with a distinct ending — no shared footer.

1. **Nav.**
2. **Hero:** h1 "Get in touch" + Newsreader 19px lead, max-width 52ch: *"Email is best, and I read everything. I'm a student, so I have more time than most people do — if you want to talk about interpretability, I'm interested."*
3. **Link cards:** dashed `border-top`, then a grid `repeat(auto-fit, minmax(min(100%,200px), 1fr))`, `gap: 18px`, `max-width: 620px`. Four cards — each an `<a>` with `display: block`, background `rgba(90,74,31,.06)`, radius 3px, `padding: 18px 20px`, containing an 11.5px uppercase eyebrow and a Newsreader 19px line:
   - Email → "Write to me →" (`mailto:gowrishkumar61@gmail.com`)
   - GitHub → "The code ↗"
   - Twitter → "@gowrishkumar23 ↗" (the only place the handle appears in full)
   - LinkedIn → "Profile ↗"
4. **"things worth writing about"** (Caveat 28px): a `<ul>`, 15.5px, `line-height: 1.8`, max-width 58ch, four items (interpretability corrections; research opportunities and reading groups; the CPU VLM benchmarks; undergrad→interpretability advice).
5. **Closing sticky note**, rotated `-.7deg`, max-width 44ch: "Based in Chennai, India. I reply to most things within a day or two."

---

## Interactions & Behavior

Minimal by design — this is a content site.

- **Navigation:** standard page links. Current page marked with dark ink + `1.5px solid #5a4a1f` bottom border.
- **Hover:** links shift `#5a4a1f` → `#8a6f1f`. Nothing else has a hover state in the design; if you add one to the Contact cards, keep it subtle (a slight background darkening, no lift or scale).
- **External links:** GitHub, Twitter, LinkedIn. Add `target="_blank" rel="noopener noreferrer"`. The `↗` glyph already marks them.
- **Disabled CV button:** not focusable, not a link. Consider `aria-disabled` plus visible text explaining the state.
- **No animations, transitions, loading states, forms, or client-side state.** There is no contact form — an explicit decision, since a form can't send mail without a third-party service.

## State Management

None. Every page is static. The only configurable values are the two Home flags (`showQuote`, `showWorkingOn`), which can be build-time constants.

## Responsive Behavior

Fluid, single-column at every width. It must work below 480px.

- Content column is `max-width: 780px` with `34px` side padding — no fixed widths.
- All headings use `clamp()`; don't replace with fixed sizes.
- Nav and footer link rows use `flex-wrap: wrap`.
- All grids use `repeat(auto-fit, minmax(min(100%, Npx), 1fr))` so cells go full-width on narrow screens — keep the `min(100%, …)` guard.
- `ch`-based measure caps handle line length; no media queries are needed anywhere in the design.
- Sticky-note rotations are small on purpose; they must not cause horizontal overflow at narrow widths.

## Assets

**None.** No images, icons, logos, or illustrations. All arrows (`→`, `↗`) are Unicode characters. The only external dependency is the Google Fonts stylesheet.

If a favicon is wanted, a "G" in Caveat on the paper background would fit.

## Files

In `design_files/`:

| File | Page |
|---|---|
| `Home.dc.html` | Home |
| `Research.dc.html` | Research |
| `About.dc.html` | About |
| `CV.dc.html` | CV |
| `Notes.dc.html` | Notes |
| `Contact.dc.html` | Contact |
| `support.js` | Design-tool runtime — **reference only, do not port** |

Open any `.dc.html` in a browser to see the rendered design. Read the markup for exact values; all styling is inline.

## Content Note

Every word on this site is the owner's own, arrived at over several rounds of review — particularly the anime-quote passage on Home and About, the "what's coming" plan on Research, and the empty-state copy on Notes. **Treat the copy as fixed content, not placeholder text.** If something must change for layout reasons, flag it rather than rewriting it.
