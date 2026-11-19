# 08 — Screenshots (capture guide + inventory, no binaries)
> This folder intentionally contains no PNGs. QA captures real shots from the runnable prototype (`public/index.html`) — never generated or external URLs. Missing file = pending, never claimed done. Keep demo credentials/badges visible in shots.
## Capture procedure
1. Viewport `480px` width (mobile), device scale 2x; also spot-check 360px + desktop.
2. AR full set + EN mirrors for `login/home/wizard-input/review/receipt` (toggle `EN` button, `dir` flips).
3. Show `demo` badges, `0 fees`, `demo: 777000111 / 1234` hints where present; mask real data (demo only).
4. Save as PNG exactly per inventory names below into this folder.
## Inventory (30 required)
```
S00-splash-ar.png, S01-welcome-ar.png, S02-onboarding-ar.png, S03-choose-ar.png,
S04-login-ar.png, S04-login-en.png, S04b-register-ar.png, R01-otp-ar.png,
S05-home-ar.png, S05-home-en.png, S06-wallets-ar.png, S07-input-ar.png, S07-input-en.png,
S08-review-ar.png, S08-review-en.png, S09-auth-ar.png, S10-receipt-ar.png, S10-receipt-en.png,
S11-history-ar.png, S12-notif-ar.png, S13-profile-ar.png, S14-qr-ar.png,
S15-pos-ar.png, S16-postx-ar.png, S17-drawer-ar.png, S18-sheet-ar.png,
R13-requested-ar.png, R22-limits-ar.png, R24-qrshare-ar.png, R29-refund-ar.png
```
Traceability: screen IDs S00–S18 + R map to `02_SCREEN_REGISTRY.md` and `public/BUQSH_UI_FLUTTER_HANDOFF/09_COMPLETION/SCREEN_TO_ROUTE_TRACEABILITY.md`.