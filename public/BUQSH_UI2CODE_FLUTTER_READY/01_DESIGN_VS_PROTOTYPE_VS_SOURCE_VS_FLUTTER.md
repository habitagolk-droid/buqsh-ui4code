# 01 — Design vs Interactive Prototype vs Web Source vs Flutter Specs
> Anti-misclaim notice: **this package contains zero `.dart` files and is NOT executable Flutter code.** It is a frozen web prototype + docs used to re-implement the same UI in Flutter/GetX 1:1.
| Layer | What it IS | What it is NOT | Where to find it |
|---|---|---|---|
| **1. Design** | Frozen visual truth: colors `#0C4A40/#278D5B/#D4E157`, Cairo/Tajawal, 8px grid, radii 18/24/32, shadows, component visuals, AR/EN strings, RTL/LTR rules | Not a Figma file, not editable artboards | `03_DESIGN_SYSTEM.md` + `02_SCREEN_REGISTRY.md` + `styles.css :root` |
| **2. Interactive Prototype** | Clickable demo in browser: FTU, login, 9 services, 4-stage Transfer with SmartAuth XOR, cashier POS, drawer, sheets, toast — all real DOM controls with demo data `777000111/1234`, fee `0` | Not production backend, not real money/KYC/camera/bio | Serve `public/` → `index.html` + `app.js` behavior |
| **3. Web Source** | Frozen editable source: `index.html` (IDs), `styles.css` (classes), `app.js` (state `role/lang/hideBal/filter/proAuth/smartMode`, `validatePhone/validatePin`, `goto/cgoto`, `validatePro/openReview/renderProAuthSmart/proDoConfirm/renderProReceipt`, `tafqit/mask*`), `worker/index.js` mock `/api/*` | Not to be restyled in this phase; no new screens/classes | `public/index.html`, `public/styles.css`, `public/app.js`, `worker/index.js` |
| **4. Flutter Specs** | Docs-only mapping: suggested `lib/` routes/controllers/repos, `ThemeData` from tokens, `Get.bottomSheet/snackbar`, `GetConnect` to same `/api/*`, Translations AR/EN, RTL `endDrawer` | Not Dart code, not pubspec, not tested app | `06_FLUTTER_GETX_SPEC.md` + `05_SERVICE_FLOW_MAPS.md` + `07_QA_CHECKLIST.md` |
## Demo simulations (must stay labeled demo)
- OTP `1234` (`#otpOverlay`), PIN setup/forgot/reset, camera frame (`#cameraOverlay`), KYC checkboxes (`#kycOverlay`), fingerprint 1200ms fake (`#proBioBtn`), QR scan (`BUQ-SCAN-DEMO`), cashier code `1234` (`#cashierCodeOverlay`), session totals in-memory.
- Footer/badges: `demo`, `تجريبي`, `0 fees`, `fee: 0 (server only)`, `256-bit (display only)`.
## Backend-review boundary
Fees, limits (`/api/limits`), schemas (`BUQ-YYYY-######`, ISO time), session totals, lookup PII masking, auth lockout — all **NEEDS-BACKEND-REVIEW**. Flutter must read `fee` from server and never hardcode pricing.