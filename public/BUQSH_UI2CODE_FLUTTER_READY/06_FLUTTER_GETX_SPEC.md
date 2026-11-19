# 06 — Flutter/GetX Implementation Spec (docs-only, no Dart claimed)
> Re-implement frozen web 1:1. Confirm fees/limits/schemas/session-totals with backend (**NEEDS-BACKEND-REVIEW**).
## Suggested `lib/` structure
```
lib/
  main.dart (GetMaterialApp, locale ar/en, ThemeData from 03)
  core/theme/app_colors.dart   # #0C4A40 etc verbatim
  core/theme/app_text.dart     # Cairo scale + PIN ls .6em
  core/theme/app_theme.dart
  routes/app_pages.dart        # S00-S18+R names below
  modules/ftu/ (splash/welcome/onboarding/choose controller+view)
  modules/auth/ (login, register_sheet, otp, forgot, reset, camera, kyc)
  modules/customer/ (home, wallets, wizard_input, review_sheet, auth_sheet, receipt_sheet, history, notifications, qr, profile, requested, limits, tx_details, qr_share)
  modules/cashier/ (login, code, pos_dash, pos_tx, wallets, profile, refund)
  widgets/ (wallet_card, tx_card, pro_sheet, pin_dots, demo_badge, bottom_nav, drawer, toast)
```
## Routes (web anchor → GetX name)
S00 `#ftuSplash`→`/splash`, S01 `#ftuWelcome`→`/welcome`, S02 `#ftuOnboard`→`/onboarding`, S03 `#/chose_login_or_reg`→`/choose`, S04 `#authView/#regOverlay`→`/login`, S05 `data-view=home`→`/home`, S06 `wallets`→`/wallets`, S07 `wizard`→`/wizard`, S08 `#proReviewOverlay`→`reviewSheet`, S09 `#proAuthOverlay`→`authSheet`, S10 `#proReceiptOverlay`→`receiptSheet`, S11 `history`→`/history`, S12 `notifications`→`/notifications`, S13 `profile`→`/profile`, S14 `qr`→`/qr`, S15 `data-cview=dash`→`/pos`, S16 `tx`→`/pos-tx`, S17 `#sideDrawer`→`endDrawer` (RTL) / `drawer` (LTR), R-screens per `02` names. Unknown → `/home` (never blank).
## Controllers (mirror `app.js state`)
- `LocaleController`: `lang='ar'/'en'`, flips `Directionality` + re-render; persist `bq_lang`.
- `AuthController`: `role/phone/pin/pinVisible/remember`; `validatePhone()` (Arabic-digit norm, strip `00967/967/0`, 9-digit start-7), `validatePin()` (4-digit, `0000` blocked demo).
- `WalletController`: `wallets/hideBal` (`bq_hide`), carousel `PageView(viewportFraction:.82)` + dots.
- `WizardController`: `svc/proAuth/smartMode/bioBusy`; `validatePro()` gates Continue; `openReview/openAuth/proDoConfirm/renderReceipt`; bio XOR PIN; confirm waits server.
- `TxController/NotifController/SessionController/NavController/UiController`: filters/search/retry, dot, session open/close totals, drawer highlight, sheet/toast.
## Repositories (`GetConnect` → same `/api/*`)
`POST login {phone,pin,role}`, `POST register {name,phone,pin}`, `POST otp/request|verify`, `POST pin/forgot|reset`, `GET wallets|transactions|notifications|requested|limits|profile`, `POST transfer|request|deposit|withdraw|exchange|pay {wallet,to,amount,notes,store}` → `{ok, operationNumber: BUQ-YYYY-######, timestamp ISO, fee:0}` read-only, `GET|POST cashier/session`, `GET cashier/lookup?phone=`, `POST cashier/sale {phone,amount}`, `POST cashier/refund {ref,reason}`. See `worker/index.js` + `05_SOURCE_CODE/SOURCE_MANIFEST.md`.
## i18n / RTL / motion
- `Translations` AR/EN keys: appName/appSub/welcomeBack/loginTitle/roleHint/customer/cashier/phone/phoneHint/pinLabel/forgot/remember/login/orVia/bioTitle/bioSub/ready/noAccount/signupFree + service/history/wallet strings; server messages AR mostly (contract **NEEDS-BACKEND-REVIEW**).
- RTL: `endDrawer` in AR, `drawer` in EN; pill/carousel/loader mirrored; phone/PIN/ref `TextDirection.ltr`.
- Motion per `07_INTERACTIONS`: rise 450ms, pill 350ms `(.6,.1,.2,1.15)`, sheets `up 300ms r24-26`, toast 2600ms, shimmer 1.2s; respect `MediaQuery.disableAnimations`.
- Keep `demo` badges + `demo: 777000111 / 1234` + footer `secure • demo` verbatim; port `tafqit/maskName/maskMobile/copy/share/fav` logic exactly.