# eshwarnevedh.com — portfolio

Source for [eshwar-nevedh-portfolio.vercel.app](https://eshwar-nevedh-portfolio.vercel.app).

One HTML file. No framework, no build step, no bundler, no analytics, and **zero third-party
network requests** — fonts are self-hosted, images are generated ahead of time, and the one
interactive model runs entirely client-side.

## Structure

```
index.html          all markup, CSS and JS (~100 KB)
assets/
  fonts/            self-hosted woff2, latin + latin-ext subsets
  *.avif|webp|jpg   responsive image variants at 1x and 2x
  og-card.jpg       social preview
```

## Notes on the build

**Images.** Sources are downscaled to the actual rendered box at 1x and 2x and encoded to
AVIF, WebP and JPEG. `<picture>` serves the smallest format the browser accepts. The
above-the-fold payload is ~296 KB including fonts; the original version of this site shipped
7.1 MB of eagerly-loaded JPEG.

**Type.** Outfit for display, Plus Jakarta Sans for text, JetBrains Mono for labels and data —
self-hosted rather than loaded from Google Fonts, which removes a third-party request, a GDPR
question, and a render-blocking round trip. `unicode-range` splits latin from latin-ext so
English readers fetch ~169 KB. See [`assets/fonts/NOTICE.md`](assets/fonts/NOTICE.md).

**Layout.** Fluid rather than breakpointed: a `clamp()` type scale, `clamp()` spacing, and
`repeat(auto-fit, minmax(min(100%, …), 1fr))` grids that cannot overflow their container.
Container queries let the case-study definition lists and the model panel respond to their own
width instead of the viewport. Verified with no horizontal overflow from 360 px to 2560 px.
Media queries are reserved for genuine mode changes — the navigation and print.

**Motion.** Reveals use native CSS scroll-driven animation (`animation-timeline: view()`), with
IntersectionObserver only as a fallback on browsers that lack it, chosen at boot via
`CSS.supports`. The reading-depth control uses the View Transitions API so tier changes
cross-fade rather than snap. The hero canvas draws drifting sine contours, is DPR-scaled, and
pauses when scrolled out of view or when the tab is hidden. A first-visit intro plays once per
session. All of it is disabled under `prefers-reduced-motion`.

**Reading depth.** A `30 sec / 3 min / 15 min` control sets `data-depth` on `<html>`; CSS hides
tiers via `.t-brief` and `.t-deep`. The choice persists in `localStorage`. With JavaScript
disabled the attribute stays at `deep`, so everything renders.

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
