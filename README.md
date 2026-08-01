# eshwarnevedh.com — portfolio

Source for [eshwar-nevedh-portfolio.vercel.app](https://eshwar-nevedh-portfolio.vercel.app).

One HTML file. No framework, no build step, no bundler, no analytics, and **zero third-party
network requests** — fonts are self-hosted, images are generated ahead of time, and the one
interactive model runs entirely client-side.

## Structure

```
index.html          all markup, CSS and JS (~94 KB)
assets/
  fonts/            self-hosted woff2, latin + latin-ext subsets
  *.avif|webp|jpg   responsive image variants at 1x and 2x
  og-card.jpg       social preview
```

## Notes on the build

**Images.** Sources are downscaled to the actual rendered box at 1x and 2x and encoded to
AVIF, WebP and JPEG. `<picture>` serves the smallest format the browser accepts. The
above-the-fold payload is ~263 KB including fonts; the original version of this site shipped
7.1 MB of eagerly-loaded JPEG.

**Fonts.** Self-hosted rather than loaded from Google Fonts — removes a third-party request,
a GDPR question, and a render-blocking round trip. `unicode-range` splits latin from latin-ext
so English readers fetch ~154 KB. See [`assets/fonts/NOTICE.md`](assets/fonts/NOTICE.md).

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
