# 04 — Reusable Component Library (same classes only)
> Props/states mirror `app.js` functions. Fee `0` server-only. Bio and PIN never visible simultaneously (`renderProAuthSmart` XOR).
## 1. Inputs — `.input-shell` + `.field-input` + `.select-box`
- Shell: `bg #F4F6F5, border 2 transparent, r18, pad 4 6 4 12`; focus white + brand + lime ring; error red border + `#FFF5F5`. Icon tile `38x44 white r12`. Country chip white pill `🇾🇪 +967`. `select-box`: same bg `r14 pad12`.
- States: default / focus / error (msg 12.5px red) / hint 12px muted / disabled `.55`.
- IDs: `#phoneInput` (tel, max 13), `#pinInput`/`#proPin`/`#regPin` (password, numeric, max 4), `#proTo`, `#proAmount` (decimal), `#proNotes` (2-row), `#proStore` (POS only).
## 2. Wallet select / currency — `#proWallet`, `#proCurLabel`, `#proBalanceHint`
- Options text: `CUR — balance (masked)`; cur pill lime `r10 12px/900`; hint `الرصيد المتاح: X CUR`; eye `#proWalletEye.dark-eye` toggles `hideBal` (`bq_hide`).
- Logic: `renderProWallets()`; validation uses selected wallet balance; mirrors `wzWallet/wzTo/wzAmount/wzFee`.
## 3. Balance cards — `.wallet-slide`, `.ws-bal`, `.ws-eye`, `.ws-cta`
- Slide `flex 0 0 82% min 240px r20 pad16 min-h 132`, per-CUR gradient; balance 26px/900 or `••••••`; masked `****4521 • demo` ltr; eye glass btn + `تحويل سريع` lime btn → `startSvcPro('transfer')`. Carousel snap-x + dots (`8px`, on `26px`).
## 4. Action buttons — `.btn-primary/.btn-filled/.btn-ghost/.btn-outline/.pro-continue`
- Primary lime/dark `h~52 r18 16/800`; filled-dark `#0C4A40`/white; outline `2px brand`; ghost `1.5px line`; demo `2px brand` + dashed secondary; disabled `.45–.55`. Sticky `.pro-cta-wrap` (bottom 8px); `proContinue` disabled until `validatePro()` true.
## 5. Review / confirm sheets — `#proReviewOverlay`, `#proAuthOverlay`, `#sheetOverlay`
- Pro sheet white `r24 top max-h 90vh anim up .3s`; head title + X; review: amount card gradient + `.review-rows` dashed + warn `لا يمكن إلغاء العملية`; generic sheet `r26 max-h 86vh` + `.set-row #F8FAF9 r14`.
- Flow: `openReview()` (needs valid) → `openAuth()` → `proDoConfirm()` waits server → `renderProReceipt()`.
## 6. Bio / PIN SmartAuth XOR — `#proBioBtn`, `#proPin`, `#proAuthStatus`, `#proAuthFallback`
- Bio mode (if supported): finger circle 72px → processing ring lime → success green `✓ — بانتظار الخادم` → `proDoConfirm(true)`; fail → red + fallback row (`رجوع` / `استخدام PIN كبديل`); never executes without success. PIN mode: 4-digit + eye, `تأكيد` disabled until valid, `proDoConfirm(false)`.
- Status pill: `.smart-status.ok/err/info`.
## 7. Loading / success / fail — `.skeleton`, `.spinner`, `.alert`, `.empty`, `#toast`
- Skeleton shimmer 1.2s; spinner 22px border-spin `.8s`; alert success `#EBFBEE/#1F6B2E` / error `#FFF0F0/#A61E1E`; empty dashed; toast dark pill bottom 96px 2600ms; processing bar `#proProcessing`; receipt success `ok-ic 56px #1F7A33`.
## 8. Receipt templates — `.receipt-paper`, `.pro-amount-card`, `.op-num`
- Total card gradient (small cur + 30px amount + type badge); rows ref ltr bold + `.copy-btn 34px` / type / date ltr / to masked / from masked / fee `0 (server only)`; actions share (`navigator.share`/clipboard) + fav (`bq_favs`) + save/close. `tafqit()` words box + `maskName/maskMobile` must be mirrored in Flutter.