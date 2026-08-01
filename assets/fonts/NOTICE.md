# Bundled fonts

Three families are self-hosted here so the site makes no third-party network requests.
All three are licensed under the **SIL Open Font License, Version 1.1** — the full text is
in [`OFL.txt`](OFL.txt).

| Family | Copyright | Upstream |
|---|---|---|
| Cormorant Garamond | The Cormorant Project Authors, Reserved Font Name "Cormorant" | https://github.com/CatharsisFonts/Cormorant |
| Lora | The Lora Project Authors, Reserved Font Name "Lora" | https://github.com/cyrealtype/Lora-Cyrillic |
| JetBrains Mono | The JetBrains Mono Project Authors, Reserved Font Name "JetBrains Mono" | https://github.com/JetBrains/JetBrainsMono |

Only the `latin` and `latin-ext` subsets are included. `unicode-range` in `../fonts.css`
means a browser rendering English text downloads roughly 154 KB and skips the rest.
