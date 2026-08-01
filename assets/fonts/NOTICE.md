# Bundled fonts

Three families are self-hosted here so the site makes no third-party network requests.
All are licensed under the **SIL Open Font License, Version 1.1** — full text in
[`OFL.txt`](OFL.txt).

| Family | Role | Copyright | Upstream |
|---|---|---|---|
| Outfit | display / headings | The Outfit Project Authors | https://github.com/Outfitio/Outfit-Fonts |
| Plus Jakarta Sans | body / UI | The Plus Jakarta Sans Project Authors | https://github.com/tokotype/PlusJakartaSans |
| JetBrains Mono | labels / data | The JetBrains Mono Project Authors | https://github.com/JetBrains/JetBrainsMono |

Only the `latin` and `latin-ext` subsets are included. `unicode-range` in `../fonts.css`
means a browser rendering English text downloads roughly 169 KB and skips the rest.

Tamil and Malayalam in the hero fall back to the reader's system fonts (Nirmala UI, Noto
Sans Tamil / Malayalam) rather than shipping two more families.
