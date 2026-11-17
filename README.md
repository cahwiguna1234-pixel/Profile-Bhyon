# ( BHYON ) — Muhammad Afdhal Portfolio (Reconstruction)

Swiss-brutalist editorial portfolio for **Muhammad Afdhal (@bhyon)** — programmer and Islamic
family law attorney based in Jember, Indonesia. Positioned around LLM gateway infrastructure,
Swiss editorial interfaces, and Linux systems.

## Architecture note (important)

The brief asked for **Next.js**. The existing repository in this workspace is a
**React 19 + Vite 7 + TypeScript + TailwindCSS v4** single-page build (with
`vite-plugin-singlefile`), and the instruction was to *keep a compatible architecture*. The site
was therefore rebuilt on the existing Vite stack. All markup, metadata, tokens, and components
are framework-portable: moving to Next.js means copying `src/components/*` into `app/`, turning
interactive sections into `"use client"` components, and relocating `index.html` metadata into
`app/layout.tsx` `metadata`. **The Next.js / Vercel-edge claim is a site claim and is not
verified here.**

## Run

```bash
npm install
npm run dev     # development
npm run build   # production -> dist/index.html
npm run preview
```

## File list

```
index.html                 Document head: title, description, OG/Twitter, theme-color, theme boot script
public/robots.txt          index, follow + sitemap pointer
public/sitemap.xml         single-URL sitemap
public/og.png              1200x630 social card (PLACEHOLDER, AI-generated)
src/main.tsx               React entry
src/index.css              Semantic design tokens, Swiss type scale, marquee + reduced-motion rules
src/App.tsx                Page shell, landmarks, skip link, section order
src/data/content.ts        All copy, projects, specs, tech matrix, log entries
src/hooks/useSystem.ts     Theme, reduced motion, Lenis scroll engine + telemetry, clock, clipboard
src/components/ui.tsx      Section, FilterBar, Schematic SVGs, Empty/Skeleton states
src/components/TopBar.tsx  Sticky bar: wordmark, nav, clock, coordinates, invert, menu
src/components/Hero.tsx    Profile, discipline, bio, GitHub stats, telemetry readout
src/components/Work.tsx    #work — 6 projects, category filter, loading/empty/error states
src/components/Mid.tsx     #process, #specs (copy button), #stack (group filter)
src/components/End.tsx     #log, #about, #contact (validated form), footer + scroll-reactive marquee
```

## Section order (acceptance)

1. Sticky top bar · 2. Hero/profile · 3. `#work` · 4. `#process` · 5. `#specs` ·
6. `#stack` · 7. `#log` · 8. `#about` · 9. `#contact` · 10. Footer + marquee.

## INFERRED items

Everything below is reconstruction, not verified source data. Each is marked `INFERRED` in code.

- **Colour palette** — only `#0a0a0a` (theme-color) is verified. `--color-surface`, `--color-text`,
  `--color-muted`, `--color-border`, `--color-accent` (`#ff3b00`) and the light theme are inferred.
- **Typeface** — the source uses fluid `clamp()` Swiss typography; the exact family is unknown.
  A neutral grotesk stack (Helvetica Neue / Arial / system grotesk) is used, no webfont download,
  so `font-display` is not applicable.
- **GitHub statistics** (repos, followers, stars, contributions) and per-project star/fork counts.
- **Project summaries and capability bullets** — paraphrased, not verbatim.
- **Workstation spec rows** `TERMINAL` and `NETWORK`.
- **Engineering log dates** 2024.06 → 2026.01 and their descriptions.
- **Pillar metrics**, `ENGINE v2.6.1`, and the Bandung coordinate readout in the top bar.
- **Schematic figures** (FIG 00.A, A-01…A-06) — redrawn simple line SVGs, not copies.

## UNVERIFIED site claims (labelled in the UI)

- "latency < 2 ms" on the gateway (shown on card A-01 as an unverified claim).
- "99.9 % uptime" (shown in the Infrastructure pillar as an unverified claim).
- Next.js + Vercel SSR/edge deployment.

All numeric telemetry is labelled **"per tanggal pengambilan 26 Oktober 2026"**.

## Placeholder assets for the owner to replace

| Asset | Status |
| --- | --- |
| `public/og.png` | AI-generated placeholder — replace with the official 1200×630 card |
| `( BHYON )` wordmark | Text placeholder only. No logo file was copied; request the official SVG |
| Favicon | Not supplied — add `public/favicon.svg` and link it in `index.html` |
| GitHub badge panel | Static text; no third-party badge images are embedded |
| Project links | All point to the GitHub profile root; replace with per-repo URLs |

## Interaction & accessibility

- **Smooth scroll:** Lenis `lerp: 0.08`, driven by a single rAF loop; anchors route through
  `lenis.scrollTo` so in-page navigation stays smooth and moves focus to the target section.
- **Marquee:** CSS animation whose `--marquee-duration` is derived from live scroll velocity.
- **Telemetry:** scroll percentage, velocity, and UTC+7 clock update in real time and are
  `aria-hidden` where decorative.
- **Reduced motion:** `prefers-reduced-motion: reduce` disables Lenis (native scroll), stops the
  marquee, removes the blinking indicator, and collapses all transitions.
- **Theme:** `data-theme` on `<html>`, persisted in `localStorage` (`bhyon-theme`), applied by an
  inline boot script before paint to avoid FOUC.
- Semantic `header` / `nav` / `main` / `section[aria-labelledby]` / `footer`, skip link,
  44 px minimum touch targets, visible focus rings, `aria-pressed` filters, live regions for
  copy and form feedback.

## States

- **Work:** loading skeleton → success grid → empty (filter with no matches) → error panel.
- **Tech matrix:** empty state per group.
- **Copy buttons:** idle / `COPIED TO CLIPBOARD` / copy-failed.
- **Contact form:** client-side validation with per-field errors, success and failure messages,
  always with the direct `mailto:` alternative. No backend, no secrets in the frontend.
