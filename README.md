# eshwarnevedh.com — portfolio

Source for [eshwar-nevedh-portfolio.vercel.app](https://eshwar-nevedh-portfolio.vercel.app).

One HTML file. No framework, no build step, no bundler, no analytics, and **zero third-party
network requests** — fonts are self-hosted, images are generated ahead of time, and the one
interactive model runs entirely client-side.

## Structure

```
index.html          all markup, CSS and JS (~78 KB)
assets/
  fonts/            self-hosted woff2, latin + latin-ext subsets
  *.avif|webp|jpg   responsive image variants at 1x and 2x
  og-card.jpg       social preview
```

## Notes on the build

**Images.** Sources are downscaled to the actual rendered box at 1x and 2x and encoded to
AVIF, WebP and JPEG. `<picture>` serves the smallest format the browser accepts. The
above-the-fold payload is ~200 KB including fonts; the original version of this site shipped
7.1 MB of eagerly-loaded JPEG.

**Type.** One typeface — Geist, at four sizes. Hierarchy comes from weight and colour rather
than a long size ramp: headings at 600 in near-black, de-emphasised clauses at 400 in grey,
eyebrows at 600 in oxide. Self-hosted, so the page makes no third-party request. See
[`assets/fonts/NOTICE.md`](assets/fonts/NOTICE.md).

**Imagery.** Every photograph is screened into ink in the browser from the AVIF — five different
screens, one per image: a soft AM dot screen, cross-hatch engraving, a coarse graphic screen, an
ordered Bayer dither, and a line screen. Hover any plate and it resolves back to the photograph.
Nothing is pre-rendered; the plates are drawn to canvas at device pixel ratio on load.

**Layout.** Fluid rather than breakpointed: a `clamp()` type scale, `clamp()` spacing, and
`repeat(auto-fit, minmax(min(100%, …), 1fr))` grids that cannot overflow. Container queries let
the model panel respond to its own width. Media queries handle only genuine mode changes — the
navigation and print.



**Motion.** One idea, applied everywhere: content arrives by unmasking upward via CSS
scroll-driven animation (`animation-timeline: view()`, with `animation-duration: auto` — a time
value silently breaks a progress-based timeline), and anything interactive answers with a line
wiping left to right. Nothing lifts, scales or shadows. IntersectionObserver is a fallback only,
selected at boot via `CSS.supports`. The reading-depth control uses the View Transitions API. The
hero is a live vector field — layered value-noise traced by ~900 particles, cursor-reactive,
DPR-scaled, paused when offscreen or when the tab is hidden. All of it is disabled under
`prefers-reduced-motion`.



**The interactive model.** A three-regime Markov decision process solving for a regime-aware
allocation policy. State is *(regime, currently-held portfolio)* — 3 × 66 = 198 states — because
rebalancing costs money, and without that cost term the problem decomposes into three
independent one-period optimisations and the discount rate stops mattering. Value iteration to
convergence, then a seeded 30-year simulation against a static 60/40. Headline statistics are
medians over 120 paths; the chart shows one representative path. Parameters are synthetic and
illustrative, not fitted to history.

**Accessibility.** Skip link, landmark elements, visible focus rings, `prefers-reduced-motion`
honoured throughout (the particle canvas also pauses when scrolled out of view or the tab is
hidden), all text at or above 11 px, and no contrast pair below WCAG AA.

## Local preview

```bash
python -m http.server 8787
```

Then open <http://localhost:8787>.
