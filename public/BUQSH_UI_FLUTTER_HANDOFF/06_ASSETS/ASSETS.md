# 06 — Assets (logo / icons / fonts — no binaries generated)
## Buqsh logo construction (recreate in Flutter, do not trace)
- Circle: lime `#D4E157` fill; sizes 96 (splash) / 56 (header) / 84 (desktop side) / 52 (choose) / 58–64 (drawer/profile).
- Mark: Arabic `ب` 900, color `#0C4A40`, ~55% of circle; dot: 7px dark circle bottom-center (`bottom:10px, translateX(-50%)`).
- Flutter: `Container(decoration: BoxShape.circle, color: accent)` + `Text('ب', style: Cairo 900)` + `Positioned` dot; export `@1x/@2x/@3x` 96/192/288px if raster needed in `assets/logo/`.
- Wordmark: `BUQSH بقش` 30px 900 ls 2px (بقش lime on dark); tag `صرتك الرقمية` 19px 800 lime; sub 13px `#D6EBDF`.
## Icons → lucide names (use `lucide_flutter` or inline SVG, 1:1 stroke)
Wallet `wallet`, transfer `send`, request `repeat`, e-pay `zap`, POS `shopping-cart`, deposit `arrow-down-to-line`, withdraw `arrow-up-from-line`, bills `receipt-text`, games `gamepad-2`, exchange `hand-coins`, phone `smartphone`, lock `lock-keyhole`, eye `eye`/`eye-off`, bio `fingerprint`, bell `bell`, menu `menu`, close `x`, check `check`/`check-circle-2`, copy `copy`, scan `scan-line`, contacts `contact`, fav `heart`, customer `user-round`, merchant `store`, home `house`, help `headset`, lang `languages`, faq `circle-help`, logout `log-out`, verified `badge-check`, sparkle `sparkles`, back `arrow-left`, in/out `arrow-down-left`/`arrow-up-right`, kyc `id-card`. Sizes: grid 24px, buttons 20px, chips 16px, dots N/A.
## Fonts
- Google Fonts: `Cairo:wght@400;600;700;800;900` + `Tajawal:wght@300;400;500;700;800` — links already in `index.html`.
- Flutter: add `cairo` via `google_fonts` or bundled `assets/fonts/Cairo-*.ttf` + `pubspec.yaml`; default `Cairo`, fallback `Tajawal`; keep weights/sizes per `03`.
## Store / placeholder avatars
- Six demo stores (النور/التقوى/الشفاء/الديوان/المعرفة/روف) with lucide glyphs on white 60px circle — no real logos. Recreate as `CircleAvatar(white, icon dark)`; do not hotlink external images.
- Wallet/masked chips stay text-only (`****4521` ltr).
## Export guidance
- `assets/logo/buqsh_mark.svg|png`, `assets/icons/` only if lucide package unavailable; prefer font/SVG.
- No photography; gradients via `LinearGradient` values in `03`.