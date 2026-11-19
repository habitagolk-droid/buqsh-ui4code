# 07 — Interactivity QA Checklist (execute against `public/index.html`, no layout changes)
> Mark simulations demo. Failures fall back per expected column. Test 360px / 390px / 480px / desktop + RTL + LTR (toggle `EN`).
## Auth + FTU
- [ ] Splash auto-hides ~1800ms → Welcome (or Choose/Login by `bq_ftu_seen`/`bq_session`).
- [ ] Welcome `استمرار` → Onboarding; `تخطي` → Choose.
- [ ] Onboarding swipe/dots/Prev/Next; slide 3 shows `ابدأ الآن` → Choose.
- [ ] Role pill slides Customer/Cashier; cashier shows `وضع التاجر` banner.
- [ ] Phone rejects `77123` (inline `9 أرقام يبدأ بـ 7`); accepts `777000111` + chip `+967`.
- [ ] PIN blocks letters, max 4, dots fill; eye toggles `password/text`.
- [ ] Login `777000111/1234` → Customer home toast; role cashier → code overlay `1234` → POS dash.
- [ ] `demo login` / `merchant demo` / `copy` buttons work; bio button runs `...→✓` then logs in.
- [ ] Register: name/phone/PIN-match validated; wrong OTP ≠ `1234` shows `OTP demo: 1234`.
## Customer
- [ ] Wallet carousel swipes, dots update, eye hides `••••••` and persists (`bq_hide`); `تحويل سريع` opens transfer Input.
- [ ] All 9 services open wizard with correct title (`svc` map) and endpoint; POS shows `store` field only.
- [ ] Wizard: Continue disabled until valid; over-balance shows `الرصيد غير كافٍ`; `tafqit` words update; fee `0 (server only)`.
- [ ] Shortcuts: scan fills `BUQ-SCAN-DEMO`; fav/contacts fill demo numbers.
- [ ] Review shows masked `*** • ****0111 (demo)` + wallet + fee 0 + warn; Cancel → Input kept; OK → Auth.
- [ ] SmartAuth XOR: only bio OR PIN visible; bio success → `بانتظار الخادم` → receipt; bio cancel/fail → fallback row, NO execute; PIN needs 4 digits to enable `تأكيد`.
- [ ] Receipt: total + ref `BUQ-YYYY-######` + copy (clipboard) + share + fav; close refreshes history.
- [ ] History chips (الكل/وارد/صادر) + search filter; empty `لا نتائج`; card → receipt.
- [ ] Notifications `read` clears dot; QR `scan demo` → e-pay Input; Profile rows open sheets/views.
## Cashier + drawer + sheets
- [ ] Session open → `open`, totals reset; charge increments totals/count; close keeps totals.
- [ ] Lookup invalid phone → toast stays; valid → masked customer card + Charge revealed.
- [ ] Refund without ref → toast; with ref → `RFN-*` card (flag backend).
- [ ] Drawer opens/closes (menu/X/scrim/Esc), active row highlighted, lang toggles dir, logout → confirm → Choose.
- [ ] Generic/info sheets close on X/scrim/Esc; toast holds 2600ms; unknown route → home fallback.
- [ ] Reduced-motion: no anim; 360px: no horizontal clip, rows wrap; LTR: drawer left, phone still ltr.