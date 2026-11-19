# BUQSH UI — Flutter Handoff Master (Zero UI Change)
> **Freeze rule:** Approved web UI is FROZEN. Do not change colors, layout, texts, or remove screens. This package is docs-only.
> Brand: `#0C4A40` / `#278D5B` / `#D4E157` — Font: Cairo (Tajawal fallback) — RTL default `dir="rtl"`.
> Demo credentials: `777000111 / 1234` — every badge `demo` / `تجريبي` must be kept in Flutter port.
> Flags: anything about **fees / limits / API schemas / auth lockout = NEEDS-BACKEND-REVIEW**.
## 1. Package map
| Folder | Contents |
|---|---|
| `BUQSH_UI_FLUTTER_HANDOFF/01_SCREENSHOTS/README.md` | Capture guide (text-only, no binaries) |
| `BUQSH_UI_FLUTTER_HANDOFF/02_SCREEN_SPECIFICATIONS/01_AUTH_FTU_SPECS.md` | Splash / Welcome / Onboarding / Choose / Login / Register |
| `BUQSH_UI_FLUTTER_HANDOFF/02_SCREEN_SPECIFICATIONS/02_CUSTOMER_APP_SPECS.md` | Home / Wallets / Input-Review-Auth-Receipt / History / Notifications / QR / Profile |
| `BUQSH_UI_FLUTTER_HANDOFF/02_SCREEN_SPECIFICATIONS/03_CASHIER_DRAWER_SPECS.md` | Cashier POS + Drawer + Sheets/Toast/Nav |
| `BUQSH_UI_FLUTTER_HANDOFF/03_DESIGN_SYSTEM/DESIGN_TOKENS.md` | Tokens extracted verbatim from `styles.css` |
| `BUQSH_UI_FLUTTER_HANDOFF/04_USER_FLOWS/FLOWS.md` | 3× mermaid flows + steps |
| `BUQSH_UI_FLUTTER_HANDOFF/05_SOURCE_CODE/SOURCE_MANIFEST.md` | Frozen source pointer (no duplication) |
| `BUQSH_UI_FLUTTER_HANDOFF/06_ASSETS/ASSETS.md` | Logo / lucide / fonts |
| `BUQSH_UI_FLUTTER_HANDOFF/07_INTERACTIONS/INTERACTIONS.md` | Sheets / drawer / motion |
| `BUQSH_UI_FLUTTER_HANDOFF/08_IMPLEMENTATION_NOTES/NOTES.md` | Done vs TODO + GetX checklist |
Canonical sources (do not edit from this package):
- `public/index.html` — DOM ids
- `public/styles.css` — tokens
- `public/app.js` — validation + state + fetch
- `worker/index.js` — mock `/api/*` contracts
## 2. Screen → route → source table
| # | Screen ID | Web route / hash | Source anchor |
|---|---|---|---|
| S00 | splash | initial overlay, auto-hide ~1800ms | `#ftuSplash` in `index.html`, `hideSplash()` in `app.js` |
| S01 | welcome | FTU step 1 | `#ftuWelcome`, `#ftuContinue`, `#ftuWelcomeSkip` |
| S02 | onboarding | FTU step 2 (3 slides) | `#ftuOnboard`, `#ftuTrack`, `#ftuDots`, `#ftuPrev/Next/Start` |
| S03 | choose_login_or_reg | `#/chose_login_or_reg` | `#chose_login_or_reg`, `#ftuLoginBtn`, `#ftuRegBtn` |
| S04 | login-register | `#/login` | `#authView`, `#tabCustomer/#tabCashier`, `#loginForm`, `#regOverlay` |
| S05 | home | customer `data-view="home"` | `#customerApp`, `#walletStrip`, `#serviceGrid`, `#recentList`, `#storesStrip` |
| S06 | wallets | customer `data-view="wallets"` | `#walletDetails`, `#proWallet` |
| S07 | wizard-input | customer `data-view="wizard"` | `#proWallet/#proTo/#proAmount/#proNotes/#proStore`, `#proContinue` |
| S08 | wizard-review | overlay | `#proReviewOverlay` |
| S09 | wizard-auth | overlay | `#proAuthOverlay`, `#proPin`, `#proBioBtn` |
| S10 | wizard-receipt | overlay | `#proReceiptOverlay` |
| S11 | history | customer `data-view="history"` | `#historyList`, `#historyChips`, `#historySearch` |
| S12 | notifications | customer `data-view="notifications"` | `#notifList`, `#notifDot` |
| S13 | profile | customer `data-view="profile"` | `#profileName/#profilePhone/#profileAvatar` |
| S14 | qr | customer `data-view="qr"` | scanner frame + `#simScanBtn` (demo only) |
| S15 | pos-dash | cashier `data-cview="dash"` | `#cashierApp`, `#sessionCard`, `#posAmount/#posPhone/#posLookup/#posCharge` |
| S16 | pos-tx | cashier `data-cview="tx"` | `#cashierTxList` |
| S17 | drawer | global RTL drawer | `#sideDrawer`, `[data-drawer-go]`, `[data-drawer-act]` |
| S18 | sheets | global | `#sheetOverlay/#sheetBody`, `#toast`, footer `#privacyBtn` |
## 3. Flutter / Dart + GetX suggestion (structure only, no UI redesign)
```
lib/
  main.dart (GetMaterialApp, locale ar/en, ThemeData from DESIGN_TOKENS.md)
  core/theme/app_theme.dart
  core/theme/app_colors.dart  // #0C4A40 etc verbatim
  core/theme/app_text.dart    // Cairo scale
  routes/app_pages.dart       // S00..S18 names above
  modules/ftu/ (splash/welcome/onboarding/choose controllers+views)
  modules/auth/ (login_controller, register_sheet)
  modules/customer/ (home/wallets/wizard/history/notifications/qr/profile)
  modules/cashier/ (session_controller, pos_view)
  widgets/ (wallet_card, tx_card, pro_sheet, pin_dots, demo_badge)
```
- State: `GetxController` + `Rx` mirroring `state` object in `app.js` (role/lang/hideBal/filter).
- i18n: `Translations` keys from `02 specs` AR/EN tables; keep `dir rtl` for `ar`.
- HTTP: `GetConnect` to same `/api/*` paths; treat `fee:0` as server-driven **[NEEDS-BACKEND-REVIEW]**.
- Sheets: `Get.bottomSheet()` with scrim `rgba(3,30,27,.55/.6)`, radius top 24–26px (see INTERACTIONS.md).
## 4. Brand / font / RTL summary
- Header gradient `linear-gradient(160deg,#0C4A40,#0E5A4F 60%,#14705F)`; radius bottom 28px; wave 30px.
- CTA lime `#D4E157` text `#0C4A40`; secondary ghost white/border `#E5ECEA`.
- Font Cairo 400/600/700/800/900, Tajawal fallback; titles 20–26px 800–900, body 13–14px.
- RTL default; drawer slides from right in RTL, left in LTR; icons mirror except logo/QR/scan.
- Keep `demo` badges + `0 fees` + `256-bit` footer labels verbatim.
## 5. Backend-review flags (do not invent)
- Fees always `0` from server — **NEEDS-BACKEND-REVIEW** before real pricing.
- Limits (e.g. 1,000,000,000 demo cap), session totals, wallet balances — **NEEDS-BACKEND-REVIEW**.
- `/api/login|register|wallets|transactions|transfer|exchange|pay|cashier/*` response shapes are demo mocks — confirm with backend before Flutter release.
- No real KYC / camera scan / biometric — demo simulation only.