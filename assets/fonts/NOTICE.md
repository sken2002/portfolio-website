# Bundled fonts

Geist is self-hosted here so the site makes no third-party network requests.
It is licensed under the **SIL Open Font License, Version 1.1** — full text in
[`OFL.txt`](OFL.txt).

| Family | Role | Copyright | Upstream |
|---|---|---|---|
| Geist | everything | The Geist Project Authors | https://github.com/vercel/geist-font |

Only the `latin` and `latin-ext` subsets are included. `unicode-range` in `../fonts.css`
means a browser rendering English text downloads roughly 125 KB and skips the rest.

Tamil and Malayalam in the hero fall back to the reader's system fonts (Nirmala UI, Noto
Sans Tamil / Malayalam) rather than shipping two more families.
