# ACTUAL_SCREENSHOTS — Real Capture Guide (text-only, no binaries)
> Never commit generated/fake images. Capture on real device/browser at 480px mobile (+ desktop spot-check). Keep demo badges + 0-fees labels visible.
## Folder convention
`public/BUQSH_UI_FLUTTER_HANDOFF/01_SCREENSHOTS/ACTUAL_SCREENSHOTS/` — files only, no subfolders.
Naming: `{ID}-{slug}-{lang}.png` e.g. `S00-splash-ar.png`, `S04-login-en.png`, `S07-input-ar.png`, `R01-otp-ar.png`, `R29-refund-ar.png`.
## Checklist (AR mandatory, EN for starred)
- [ ] S00 splash (during 1800ms) • S01 welcome • S02 onboarding ×3 • S03 choose • *S04 login AR+EN + cashier banner • R01 OTP • R02/R03 signup+PIN • R04/R05 forgot+reset • R06 camera • R07 KYC
- [ ] *S05 home AR+EN • S06 wallets • R08 wallet-details • *S07 input AR+EN • *S08 review • S09 auth • *S10 receipt • S11 history • S12 notif • S13 profile • S14 qr • R11 txdetails • R13 requested • R22 limits • R24 qr-share
- [ ] S15 pos-dash • S16 pos-tx • S17 drawer • S18 sheet • R26 ccode • R27 cwallets • R29 refund
## Steps
1. `bun run dev` → mobile 390×844 (or 480px) RTL AR; login demo 777000111/1234.
2. Screenshot each route (goto/cgoto per traceability); show processing + success + one error state for wizard.
3. Switch EN (drawer lang) → recapture starred; verify dir=ltr, phone stays ltr.
4. Desktop ≥1024px: capture home + drawer to prove side-brand.
5. Link filename into SCREEN_TO_ROUTE_TRACEABILITY Screenshot column; missing = `pending`.
## Rules
- No cropping of badges/footer; no real PII (mask ****); reduced-motion off for motion shots; do not edit colors/fonts.