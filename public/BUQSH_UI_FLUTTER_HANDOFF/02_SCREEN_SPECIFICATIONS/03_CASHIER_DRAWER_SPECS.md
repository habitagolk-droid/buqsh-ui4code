# 02.3 — Cashier POS + Drawer + Global Sheets/Toast/Nav
> Source: `#cashierApp .cview[data-cview]` + `#sideDrawer` + `#sheetOverlay` + `#toast`. APIs: `/api/cashier/session|lookup|sale`. Session totals **NEEDS-BACKEND-REVIEW**.
## Role + entry
- Login with `role=cashier` (pill `كاشير / تاجر` + `merchantBanner`); `enterApp()` toggles `#customerApp`/`#cashierApp`; header hello becomes `لوحة التاجر`, badge `كاشير • تجريبي`; toast `مرحباً أيها التاجر`.
## S15 POS Dash `data-cview="dash"`
- Session card white `r20 pad14`: label `session` + value `open/closed` + meta total/count + CTA `open/close` (`btn-primary` auto width `11 18`).
  - `POST /api/cashier/session {action:open|close}` → `{session{open,total,count}}`; totals accumulate locally in mock (`total+=amt`) — flag backend.
- Sale card: `amount` decimal + `phone` Yemen rule (rtl-styled ltr) + `lookup` primary → `GET /api/cashier/lookup?phone=` → review card dashed (`customer • displayName ***`) + reveals `charge`; `charge` → `POST /api/cashier/sale {phone,amount}` → receiptHtml (`BUQ-YYYY-######`, fee 0) in `#posResult` + session update + `loadCashierTx()`.
- Recent: `#posRecent` (id in JS; HTML anchor `#posRecent` — if missing in markup, Flutter still shows 8-item `tx-card` list; note as **NEEDS-BACKEND-REVIEW** for id parity) max 8, tap → receipt.
- Bottom nav cashier: 2 cols max 360px (`sales/tx`), active same style.
## S16 POS Tx `data-cview="tx"`
- List `#cashierTxList` same `tx-card`; no filters (keep); empty dashed `—`.
## S17 Drawer `#sideDrawer`
- RTL: `translateX(105%) right:0 r24 0 0 24`; LTR mirrored left; `.open` translate 0; overlay `rgba(3,30,27,.55)` z55/56; `aria-modal`, Esc closes.
- Header gradient + avatar 58px + name/phone + X glass btn.
- Rows (13px gaps, icon tile 40px `#EEF5F1`): profile(home icon `user-round`)→profile, home→home, history→history, notif→notif, QR→qr, wallets→wallets, lang (`العربية` pill → toggles ar/en), support→info sheet, faq→info sheet, logout danger red → confirm sheet (`تسجيل الخروج؟ (تجريبي)` → `logout()` clears `bq_session`, routes to choose/welcome).
- Active row: `bg #EDF4F1 + inset border-start 4px dark` via `highlightDrawer()`; `goto()` never blank-screens (unknown → home fallback + warn).
## S18 Global sheets / toast / nav
- Generic sheet: scrim fixed, sheet `min(480px,100%) r26 top pad12 16 26 max-h86vh`; head title + X; body `set-row(white? #F8FAF9 r14)` lists; click scrim/Esc closes.
- Info sheets `openInfoSheet(kind)`: support (hotline `800-1234` + WhatsApp demo + `0 fees • demo • 256-bit`), faq (fees 0 / demo login / PIN 4), terms/privacy demo one-liners, language (العربية/English ✓), kyc toast-only `التوثيق تجريبي — قريباً`.
- Language special: `goto('language')` toggles directly (no sheet); drawer `lang` act same.
- Toast: fixed bottom 96px centered pill dark, `show` 2600ms + fade; icons `check-circle-2`.
- Security footer: `secure • demo` + privacy link; `helpBtn` → toast `800-1234`.
- Motion/timing in `07_INTERACTIONS`; reduced-motion disables all.