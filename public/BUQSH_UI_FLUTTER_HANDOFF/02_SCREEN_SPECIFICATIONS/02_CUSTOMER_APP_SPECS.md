# 02.2 — Customer App Specs (Home / Wallets / Services Flow / History / Notifications / QR / Profile)
> Source ids: `#customerApp .cview[data-view]` + `#pro*` overlays. APIs: `/api/wallets`, `/api/transactions`, `/api/transfer|request|deposit|withdraw|exchange|pay`. Fee always `0` server-only — **NEEDS-BACKEND-REVIEW**.
## Shell + pro header
- `.pro-header`: gradient `#0C4A40→#126350→#278D5B`, `r22 pad14`, deco circle lime .16; row: menu btn + user (avatar 48px lime-bordered + hello 12px `#D6EBDF` + name 17px 800 + role badge lime pill) + bell/QR 42px glass btns; `notifDot` red 10px if unread.
- Bottom nav: fixed bottom 10px, `min(460px,100%-20px)`, white .97, `r22`, 5 cols; active `#EDF4F1` + dark; center QR FAB 44px dark circle -22px offset + border white.
- Footer: `secure • demo` + privacy link; padding bottom `nav-h+28`.
## S05 Home `data-view="home"`
1. **Wallets carousel** `#walletStrip`: horizontal snap, gap 12, slide `flex 0 0 82% min 240px r20 pad16 min-h 132`; gradients YER `#0C4A40→#1a7a65`, SAR `#0B3B54→#14705F`, USD `#1C4D2A→#278D5B`; top row name 12.5px + cur pill glass; balance 26px 900 (or `••••••` when `hideBal` persisted `bq_hide`); masked `****4521 • demo` ltr; foot: eye glass btn + `تحويل سريع` lime btn → `startSvcPro('transfer')`; dots + count line `N محافظ • YER / SAR / USD`.
   - Loading: single glass skeleton; Empty: dashed `لا توجد محافظ`; Error: fallback `125000/2300/540` demo + `walletsError` flag (keep).
2. **Services 3×3** `#serviceGrid`: white cards `r18 pad14`, icon tile 48px `#EEF5F1` 24px dark icon, label 13px 800. Map: تغذية/حوالة/تحويلات/إلكتروني/POS/سحب/فواتير/ألعاب/شبكي → svc keys deposit/transfer/request/pay_elec/pos/withdraw/bills/games/exchange; `deposit/withdraw/bills/games` currently route to `transfer` (preserve, do not invent).
3. **Recent** `#recentList`: tools search + chips (الكل/وارد/صادر/فواتير); `tx-card(white r18 pad12, ic 36px up green/down red, title 13.5px 800 ellipsis, sub 11.5px muted, amt green/red)`; tap → receipt sheet; retry `↻` on empty-load fail; limit 5.
4. **Stores strip** `#storesStrip`: 76px items, logo 60px circle white, tap prefills `proStore` + opens `pos` flow.
- Texts: walletsTitle/servicesTitle/recentTitle/viewAll/searchPh.
## S06 Wallets `data-view="wallets"`
- Detail container `#walletDetails` + same select `#proWallet` options `CUR — balance (masked)`; eye `#proWalletEye.dark-eye`; hint `الرصيد المتاح: X CUR`; cur pill `#proCurLabel`.
- Validation uses selected wallet balance; over-balance → `balance` error (message backend-review).
## S07–S10 Services flow (Input → Review → Auth → Receipt)
- **Input** `#proInputCard` (top border 4px dark): flow tag `demo + label(تحويل إلى مشترك/شبكي/دفع نقاط البيع...)`; wallet row select + eye; balance hint; `to` label + shell shortcuts (scan→`BUQ-SCAN-DEMO`, fav, contacts) — phone Yemen rule except `exchange` (free text, `required` only); `store` field only for POS; amount shell `#F0F7F4` input 24px 900 dark + cur pill lime; `tafqit` Arabic words box (`X ريال يمني/سعودي/دولار فقط لا غير`, `—` if 0); notes 2-row; fee line `fee: 0 (server only)`; sticky `استمرار` dark CTA disabled until valid; `back` ghost → home. Hidden mirrors `wzWallet/wzTo/wzAmount/wzFee`.
- **Review** `#proReviewOverlay`: amount card gradient (cur small + amount 30px 900 + type badge); rows to(masked `Ahmed *** • ****0111`)/wallet/fee 0/notes optional; `cancel` outline + `ok` filled → auth.
- **Auth** `#proAuthOverlay`: fingerprint circle 72px → demo `...→✓` 1200ms + toast; OR PIN 4 (prefilled demo) + eye; `confirm` filled → `POST {wallet,to,amount,notes,store}` to `/api/transfer|exchange|pay` by svc; on ok builds receipt `{operationNumber,date,amount,currency,fee:0}`; errors toast `failed` (backend-review).
- **Receipt** `#proReceiptOverlay`: total card + rows ref(ltr `op-num` + copy btn)/to/from/fee 0; actions share (`navigator.share`/clipboard) + fav (`bq_favs`) + close; also generic `receiptHtml()` for history tap with `Copy/Share`.
- Copy/share/fav/tafqit/masking (`maskName/maskMobile`) must be ported verbatim.
## S11 History `data-view="history"`
- Chips الكل/وارد/صادر + search `بحث بالاسم أو رقم العملية...`; list full (no 5-cap); empty `لا نتائج` dashed; card tap → receipt.
## S12 Notifications `data-view="notifications"`
- Head + `read` (marks all read, clears dot); cards title+time, non-clickable; empty `—`.
## S14 QR `data-view="qr"`
- White card `r-xl pad22` centered `scan-line 48px` + `scan demo` primary → `startSvcPro('pay_elec')`. No real camera (demo-only, do not add).
## S13 Profile `data-view="profile"`
- Hero gradient card: avatar 64px lime-bordered + name + `+phone` ltr; rows via drawer (profile/history/notif/qr/wallets) — keep same labels.