# 02.1 — FTU + Auth Specs (Splash / Welcome / Onboarding / Choose / Login / Register)
> Source: `public/index.html` + `public/app.js` + `public/styles.css` + `worker/index.js`.
> Brand `#0C4A40` / `#278D5B` / `#D4E157`, font Cairo/Tajawal, RTL default. Demo `777000111 / 1234`.
> Server messages / fees / limits = **NEEDS-BACKEND-REVIEW**.
## Global auth card
- Layout: `.app-shell(max 480px)` → `.app-header(sticky, r 0 0 28 28)` → `.main-area(margin-top:-28, r 28 28 0 0, pad 18 14)` → `.login-card(white, r 32, pad 22 18, shadow --sh, grip 48×5)`.
- Type: kicker 13px 700 `#0C4A40` + title 23px 800 `#003E47` + sub 13.5px `#6B7D7D`.
- Spacing: 8px grid (`space 4/6/8`); fields `p-4`-ish, `rounded-2xl` (18px).
- Focus: input shell border `#0C4A40` + ring `0 0 0 4px rgba(212,225,87,.6)`; error: border `#E5484D`, bg `#FFF5F5`, msg 12.5px `#C92A2A`.
- CTA `.btn-primary` lime bg, dark text 16px 800, h ~52px, hover `#DEEB7A`, spinner 22px.
- RTL: `dir=rtl` root; phone input `dir=ltr` visually right-aligned; LTR mode mirrors paddings/drawer only.
- States: loading spinner in CTA + disabled; success green alert; error red alert + inline hints; empty N/A.
## S00 Splash `#ftuSplash`
- Goal: branded launch veil ~1800ms, then `ftuDecide()` by `bq_ftu_seen` + `bq_session`.
- Layout: fixed inset 0, gradient `#0C4A40→#278D5B`, centered max 320px; logo 96px lime circle `ب`+dot; brand 30px 900 ls 2px (`بقش` lime); tag 19px; sub 13px `#D6EBDF`; loader 120×6 bar 40% lime anim `ftuLoad` (LTR mirrored).
- Texts AR: `BUQSH بقش / صرتك الرقمية / محفظة رقمية ومدفوعات سريعة وآمنة`; EN mirror via i18n (keep meaning).
- Actions: auto `fade-out` 600ms (reduced-motion: instant hide); no buttons.
- A11y: `aria-live=polite`, loader `aria-hidden`.
## S01 Welcome `#ftuWelcome`
- Goal: greet + single CTA to onboarding.
- Layout: card + `.ftu-top(demo badge + lang btn)` + kicker/title/sub + `.ftu-wallet-scene(gradient r20, two glass cards YER 125,000 + QR 0 رسوم)` + `استمرار` filled + `تخطي` ghost.
- Buttons: filled dark `#0C4A40` white text for `ftu-login` variant; here `استمرار` primary lime.
- Transitions: `rise .45s`; skip → `#/chose_login_or_reg` + `markSeen()`.
## S02 Onboarding `#ftuOnboard`
- Goal: 3 slides (wallets YER/SAR/USD — حوالات PIN/بصمة — QR رسوم 0).
- Layout: `.ftu-slider` overflow hidden; `.ftu-track` scroll-snap-x; slides 100% `r18 bg #F2F6F4`; icon tile 72px dark/lime; dots 8px (active 26px dark).
- Controls: `السابق` ghost + `التالي` filled; last slide hides next, shows `ابدأ الآن`; `تخطي` top-left; swipe updates dots (90ms debounce); keyboard focusable slider.
- RTL quirk: track `direction:ltr`, slides `direction:rtl` (AR) to keep snap math; mirror in LTR.
## S03 Choose `#chose_login_or_reg`
- Goal: fork login vs register; hash `#/chose_login_or_reg`.
- Layout: choose-head (logo 52px + title 20px + sub) + `تسجيل الدخول` filled-dark w/ `log-in` icon + `أنشئ حساباً مجانياً` outline + `demo: 777000111 / 1234` ltr hint.
- Actions: login → `#/login` + `showFtu('login')`; register → `openRegister()` sheet.
## S04 Login `#authView`
- Goal: role + phone + PIN → `POST /api/login`.
- Role switch: 2-col grid `bg #EFF3F2 r18 pad5`; sliding `#rolePill` dark animated 350ms; active white text; `aria-selected`.
- Merchant banner (cashier only): gradient dark→green, icon tile lime `badge-check`, `وضع التاجر / QR + sales (demo)`.
- Phone: label `رقم الجوال`; shell icon `smartphone` + input `tel 17px 700` + chip `🇾🇪 +967`; hint 12px muted; validation: strip `00967/967/0`, must be 9 digits start `7` (`validatePhone`); error inline + shell red.
- PIN: label + `نسيت الرقم؟` link (demo toast); shell icon `lock` + `password` input centered ls `.6em` max 4 numeric (Arabic digits normalized) + eye toggle; dots 4×44×8 bar (`.on` dark).
- Remember: custom 22px checkbox dark/lime, default checked → persists `bq_session`.
- Submit: `تسجيل الدخول + arrow-left`; loading disables + spinner; demo quick buttons (`demo login`, `merchant demo`, `copy`); divider `أو تابع عبر`; bio button dashed `fingerprint 48px` + `الدخول بالبصمة` + `جاهز` pill → 5-step scan anim → `quickDemoLogin()`.
- API: `{phone:'967'+core, pin, role}` → `{ok, token, user{name,phone,role}}`; fallback: if core `777000111`+`1234` enter demo locally. Errors: 400 invalid / 401 wrong `0000` blocked — **NEEDS-BACKEND-REVIEW** for lockout text.
- i18n keys: appName/appSub/welcomeBack/loginTitle/roleHint/customer/cashier/phone/phoneHint/pinLabel/forgot/remember/login/orVia/bioTitle/bioSub/ready/noAccount/signupFree.
## S04b Register `#regOverlay`
- Goal: `POST /api/register {name, phone, pin}`.
- Layout: bottom sheet `r24 top only, max-h 90vh, anim up .3s`; head `إنشاء حساب جديد` + X; demo line; fields name (≥2 chars) / phone (same Yemen rule) / PIN 4 (block `0000`); footer `إلغاء` ghost + `إنشاء الحساب` filled; secure note `demo • 256-bit`.
- Fallback: on fetch fail still enters demo customer + toast `تم إنشاء حساب تجريبي` (keep behavior, flag backend).