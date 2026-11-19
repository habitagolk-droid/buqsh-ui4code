# 03 — Frozen Design System (verbatim from `public/styles.css`)
> Copy values exactly into Flutter `ThemeData`. Missing/new token → **NEEDS-BACKEND-REVIEW**. No new hex.
## Colors (`:root`)
| Token | Value | Usage |
|---|---|---|
| `--brand` | `#0C4A40` | header, pill, CTA-dark, icons |
| `--brand-deep` | `#08332C` | bg gradient end |
| `--accent` | `#D4E157` | primary CTA bg, logo, badges |
| `--accent-d` | `#AFCF3A` | focus/shadow base |
| `--accent-hi` | `#DEEB7A` | CTA hover |
| `--bg` | `#F8F9FA` | main-area |
| `--surface` | `#FFFFFF` | cards, sheets, nav |
| `--title` | `#003E47` | headings |
| `--ink` | `#10201D` | body |
| `--muted` | `#6B7D7D` | hints |
| `--line` | `#E5ECEA` | borders |
| `--err` | `#C92A2A` | error text |
| `--ok` | `#1F7A33` | success |
| demo badge | `bg #FFF4CC / border #E8D48B / text #7A5B00 / r99 / 10.5px/800` | keep on all demo surfaces |
Gradients: header `linear-gradient(160deg,#0C4A40,#0E5A4F 60%,#14705F)`; pro-header `150deg #0C4A40,#126350 55%,#278D5B 100%`; wallets YER `140deg #0C4A40,#1a7a65`, SAR `140deg #0B3B54,#14705F`, USD `140deg #1C4D2A,#278D5B`; scrims `rgba(3,30,27,.55/.6)`.
## Typography (Cairo primary, Tajawal fallback)
Import `Cairo 400/600/700/800/900` + `Tajawal 300/400/500/700/800`. Scale: brand 22/800, welcome-title 23/800, sub 13.5, label 13.5/700, input 17/700, CTA 16/800, balance 26/900, receipt 30/900, small 11–12.5/700–800. PIN `letter-spacing .6em` centered.
## Spacing / radii / shadows
8px grid; card pad `22 18`; sec-head margin `12 0 8`; nav-h `76px`; main pad `18 14 28`. Radii: `--r-lg 18`, `--r-xl 24`, `--r-2xl 32`; buttons 14–18; chips 99; sheets top 24–26; drawer side-only 24. Shadow `--sh: 0 18px 50px rgba(12,74,64,.14)`; CTA `0 10px 24px rgba(175,207,58,.4)`; nav `0 14px 34px rgba(0,0,0,.14)`. Grip `48x5 r99 #E3E9E7 mb14`. Focus: border brand + `0 0 0 4px rgba(212,225,87,.6)`.
## RTL / LTR
Default `dir=rtl lang=ar`. Drawer side (RTL right / LTR left), role-pill slide direction, loader keyframes, `phone-shell` padding flip. Phone/PIN/ref stay `dir=ltr`. Mirror rows/icons; do NOT mirror logo `ب`, QR art, numeric refs.