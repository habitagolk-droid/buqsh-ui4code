# 08 — Implementation Notes (done vs TODO, demo warnings, GetX checklist)
## Done (ported 1:1 to Flutter, keep as-is)
- [x] FTU: splash 1800ms + welcome + 3-slide onboarding + choose + hash `#/chose_login_or_reg` + `bq_ftu_seen`
- [x] Auth: role pill customer/cashier, Yemen phone (`+967`, 9-digit start-7, Arabic-digit norm), 4-digit PIN + dots + eye, remember (`bq_session`), demo `777000111/1234`, bio simulation, register sheet + `POST /api/register` with demo fallback
- [x] Customer: pro-header, wallet carousel YER/SAR/USD + hide (`bq_hide`), 3×3 services, recent (5 + filters + search + retry), stores strip, wallets detail, Input→Review→Auth→Receipt with tafqit/masking/copy/share/fav, history + search/chips, notifications + dot, QR demo, profile hero
- [x] Cashier: session open/close, lookup masked customer, sale + receipt, tx list, 2-tab nav
- [x] Global: RTL/LTR + AR/EN i18n, drawer + active state, generic/info sheets, toast, footer, skeletons, reduced-motion
## NOT done / out of scope (do NOT invent in Flutter)
- Real KYC / ID upload review, real camera QR scan, real fingerprint (all demo simulations)
- Real fees/pricing, real limits/quotas, real balances/persistence, push notifications
- Backend session/auth hardening (lockout, OTP, token refresh) — UI shows demo messages only
## Demo warnings (keep visible in app + store listing)
> `تجريبي — demo • 0 fees • 256-bit (display only)`. No real money moves. Credentials `777000111 / 1234` are public demo. `0000` PIN intentionally rejected in mock.
## NEEDS-BACKEND-REVIEW (must confirm before release)
| Item | Web today | Ask backend |
|---|---|---|
| Fees | always `0` server field | real fee table per rail/currency |
| Limits | `>1e9` blocked demo-only | min/max/step per wallet + daily caps |
| Auth | `0000` 401, others pass demo | lockout, attempts, expiry, messages AR/EN |
| Schemas | mock `FALLBACK_WALLETS/TX`, `BUQ-YYYY-######`, ISO time | frozen OpenAPI + error codes |
| Session | totals accumulate in-memory | authoritative totals/count source |
| Lookup | masked `****+last4` demo | PII masking + consent rules |
| i18n | client dict, server msg AR mostly | server locale contract |
## Flutter GetX port checklist
- [ ] `ThemeData` from `03` (no new hex), Cairo via `google_fonts`/bundled
- [ ] Routes S00–S18 per master table; unknown → home (never blank)
- [ ] `AuthController(phone,pin,role,hideBal)`, `WalletController`, `TxController`, `SessionController`, `LocaleController(ar/en + dir)`
- [ ] Validators mirror `validatePhone/validatePin` incl. Arabic digits + `00967/967/0` strip
- [ ] Sheets/drawer/toast/motion per `07`; `disableAnimations` respected
- [ ] HTTP via `GetConnect` to same `/api/*`; `fee` read-only from server; no hardcoded pricing
- [ ] Keep `demo` badges + `demo: 777000111 / 1234` hints + footer
- [ ] Capture screenshots per `01` AR+EN and attach to PR; no UI diff without approval