# BUQSH_UI2CODE_FLUTTER_READY — Master Index (Docs-Only, Frozen UI)
> **Freeze rule:** S00–S18 + R screens + 4-stage Transfer (Input → Review → SmartAuth → Receipt) are FROZEN. No color/layout/text deletion. Keep all `demo` badges.
> Brand `#0C4A40` / `#278D5B` / `#D4E157` — Font Cairo (Tajawal fallback) — RTL default `dir="rtl"`, LTR supported.
> Demo credentials: `777000111 / 1234` — OTP demo `1234` — fee always `0` server-only.
> **This package is NOT Flutter code.** It is docs + frozen web prototype reference for a Flutter/GetX re-implementation. See `01_DESIGN_VS_PROTOTYPE_VS_SOURCE_VS_FLUTTER.md`.
## 1. What this project is
Editable, runnable **web prototype** (`public/`) + **docs for Flutter port** (`public/BUQSH_UI2CODE_FLUTTER_READY/` + legacy `public/BUQSH_UI_FLUTTER_HANDOFF/`). All buttons/fields/lists/sheets are real interactive DOM — not images.
## 2. Package structure
```
public/
  index.html            # frozen DOM + IDs
  styles.css            # frozen tokens + classes
  app.js                # frozen state/validation/router/fetch
  BUQSH_UI2CODE_FLUTTER_READY/
    README.md                                   # this file
    01_DESIGN_VS_PROTOTYPE_VS_SOURCE_VS_FLUTTER.md
    02_SCREEN_REGISTRY.md
    03_DESIGN_SYSTEM.md
    04_COMPONENT_LIBRARY.md
    05_SERVICE_FLOW_MAPS.md
    06_FLUTTER_GETX_SPEC.md
    07_QA_CHECKLIST.md
    08_SCREENSHOTS/README.md
worker/
  index.js              # frozen mock /api/* contracts (demo)
```
Legacy handoff (kept, do not edit): `public/BUQSH_UI_FLUTTER_HANDOFF/` + `public/BUQSH_UI_HANDOFF_MASTER.md`.
## 3. How to run the web prototype
1. Serve `public/` statically (any static server). Example: `npx serve public` or Cloudflare Worker assets (already configured).
2. Open `/` → Splash (~1800ms) → Welcome → Onboarding (3 slides) → Choose `#/chose_login_or_reg`.
3. Login: role Customer/Cashier pill → phone Yemen `777000111` → PIN `1234` → `تسجيل الدخول`. Or `demo login` / `merchant demo` buttons.
4. Transfer flow: Home → any of 9 services → Input `#proInputCard` → `استمرار` → Review `#proReviewOverlay` → `تنفيذ` → SmartAuth `#proAuthOverlay` (bio XOR PIN) → Receipt `#proReceiptOverlay`.
5. Cashier: login as cashier → code `1234` → Session open → Lookup → Charge → Refund tab.
## 4. Frozen sources (do not redesign)
| Layer | File |
|---|---|
| DOM + IDs + i18n keys | `public/index.html` |
| Tokens + classes | `public/styles.css` |
| State + validation + router + fetch | `public/app.js` |
| Mock API | `worker/index.js` |
## 5. Navigation
- Distinction: `01_DESIGN_VS_PROTOTYPE_VS_SOURCE_VS_FLUTTER.md`
- Screens: `02_SCREEN_REGISTRY.md`
- Tokens: `03_DESIGN_SYSTEM.md`
- Components: `04_COMPONENT_LIBRARY.md`
- Flows: `05_SERVICE_FLOW_MAPS.md`
- Flutter/GetX: `06_FLUTTER_GETX_SPEC.md`
- QA: `07_QA_CHECKLIST.md`
- Screenshots: `08_SCREENSHOTS/README.md`
## 6. Flags
- Fees/limits/schemas/session-totals = **NEEDS-BACKEND-REVIEW**. Never invent pricing in Flutter.
- Simulations (demo-only): KYC, camera, QR-scan, fingerprint, OTP `1234`. Keep visible `demo` / `تجريبي` labels.