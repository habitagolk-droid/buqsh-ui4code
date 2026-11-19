# 03 — Design Tokens (verbatim from `public/styles.css`, for Flutter ThemeData)
> Keep values identical. Missing/new token → **NEEDS-BACKEND-REVIEW**, do not invent.
## Colors
| Token | Value | Usage |
|---|---|---|
| `--brand` | `#0C4A40` | header, pill, CTA-dark, icons |
| `--brand-deep` | `#08332C` | bg gradient end |
| `--accent` | `#D4E157` | primary CTA bg, badges, logo |
| `--accent-d` | `#AFCF3A` | focus ring base / shadow |
| `--accent-hi` | `#DEEB7A` | CTA hover |
| `--bg` | `#F8F9FA` | main-area |
| `--surface` | `#FFFFFF` | cards, sheets, nav |
| `--title` | `#003E47` | headings |
| `--ink` | `#10201D` | body text |
| `--muted` | `#6B7D7D` | hints, secondary |
| `--line` | `#E5ECEA` | borders, dividers |
| `--err` | `#C92A2A` | error text |
| `--ok` | `#1F7A33` | success |
| header gradient | `linear-gradient(160deg,#0C4A40,#0E5A4F 60%,#14705F)` | `.app-header` |
| pro-header | `linear-gradient(150deg,#0C4A40,#126350 55%,#278D5B 100%)` | customer header |
| wallet YER | `linear-gradient(140deg,#0C4A40,#1a7a65)` | slide |
| wallet SAR | `linear-gradient(140deg,#0B3B54,#14705F)` | slide |
| wallet USD | `linear-gradient(140deg,#1C4D2A,#278D5B)` | slide |
| scrim | `rgba(3,30,27,.55/.6)` | drawer/sheet overlays |
| demo badge | `bg #FFF4CC border #E8D48B text #7A5B00 r99 10.5px 800` | keep |
## Typography (Cairo primary, Tajawal fallback)
- Import: Google Fonts `Cairo 400/600/700/800/900` + `Tajawal 300/400/500/700/800`.
- Scale: brand 22px 800 / welcome-title 23px 800 / sub 13.5px / label 13.5px 700 / input 17px 700 / CTA 16px 800 / balance 26px 900 / receipt-amount 30px 900 / small 11–12.5px 700–800.
- Flutter: `fontFamily: 'Cairo'`, fallback `'Tajawal'`; `letterSpacing` PIN `0.6em` centered.
## Spacing / radii / shadows
- Spacing 8px grid; card pad `22 18`; sec-head margin `12 0 8`; nav-h `76px`; main pad `18 14 28`.
- Radii: `--r-lg 18 / --r-xl 24 / --r-2xl 32`; buttons 14–18; chips 99; inputs 14–18; sheets top 24–26; drawer 24 (side only); avatar circle.
- Shadow: `--sh 0 18px 50px rgba(12,74,64,.14)`; CTA `0 10px 24px rgba(175,207,58,.4)`; nav `0 14px 34px rgba(0,0,0,.14)`.
- Grip: `48×5 r99 #E3E9E7 centered mb14`.
## Components
- **Buttons:** primary lime/dark `h~52 r18`; filled-dark `#0C4A40/white`; outline `2px brand/white`; ghost `1.5px line/white dark text`; demo `2px brand` + secondary dashed; disabled `.55 op`.
- **Inputs:** shell `bg #F4F6F5 border 2 transparent r18 pad 4 6 4 12`; focus `white + brand + ring lime`; icon tile `38×44 white r12 border line`; country chip white pill `+967`; select same bg `r14 pad12`; pin-dots `44×8 r99 #E6ECEA, .on brand`.
- **Wallet card:** `r20 pad16 min-h132`, top row 12.5px + cur glass pill, balance 26px, masked 12px `#D6EBDF` ltr, foot eye-glass + lime CTA 12.5px.
- **Tx card:** white `r18 pad12` row gap10, ic 36 r12 (up `#EBFBEE/#1F6B2E`, down `#FFF0F0/#A61E1E`), title 13.5 800 ellipsis, amt colored.
- **Nav:** bottom fixed/sticky white .97 `r22` 5-col (cashier 2-col), active `#EDF4F1`; QR FAB 44 dark circle offset -22 + white ring.
- **Sheet/drawer/toast:** per 02.3 + timings in 07.
## Icons (lucide names — map to `lucide_flutter` / svg)
`wallet, send, qr-code, repeat, zap, shopping-cart, arrow-down-to-line, arrow-up-from-line, receipt-text, gamepad-2, hand-coins, smartphone, lock-keyhole, eye, eye-off, fingerprint, bell, menu, x, check, check-circle-2, copy, scan-line, contact, heart, user-round, store, house, headset, languages, circle-help, log-out, badge-check, sparkles, arrow-left, arrow-up-right, arrow-down-left, id-card, phone, message-circle, shopping-basket, cross, utensils, book-open, coffee, shield-check, info, user-plus, log-in`.
## RTL / LTR
- Default `dir=rtl lang=ar`; toggle sets `documentElement.dir/lang` + re-render.
- Drawer side, pill slide direction, loader keyframes, `phone-shell` padding flip; phone/PIN/ref stay `dir=ltr` with right visual align in RTL.
- Mirror rows/icons; do NOT mirror logo `ب`, QR art, numeric refs.