# 04 — User Flows (mermaid + steps, demo paths labeled)
## F1 — First-time FTU (Splash → Welcome → Onboarding → Choose → Login/Register)
```mermaid
graph TD
  A[S00 Splash #ftuSplash ~1800ms] --> B{bq_ftu_seen?}
  B -- no --> C[S01 Welcome #ftuWelcome]
  B -- yes --> D{bq_session==1?}
  C -->|استمرار| E[S02 Onboarding #ftuOnboard 3 slides]
  C -->|تخطي| G[S03 Choose #/chose_login_or_reg]
  E -->|التالي ×2 / swipe + dots| F[slide 3: ابدأ الآن]
  F --> G
  E -->|تخطي| G
  D -- yes --> H[S04 Login #authView]
  D -- no --> G
  G -->|تسجيل الدخول| H
  G -->|أنشئ حساباً| R[S04b Register #regOverlay]
  H -->|POST /api/login ok or demo 777000111/1234| APP[App by role]
  R -->|POST /api/register ok/fallback demo| H
  H -->|error 400/401| HERR[inline + alert + retry]
  HERR --> H
```
Steps: 1) splash auto-hide (reduced-motion instant). 2) welcome scene + CTAs. 3) onboarding swipe/dots/prev-next/start. 4) choose fork + hash. 5) login role-pill + Yemen phone + 4-PIN + bio demo. 6) register sheet validation. Errors retry on same screen; `markSeen()` persists `bq_ftu_seen`.
## F2 — Customer money (Home → Wallets → Input → Review → Auth → Receipt → History)
```mermaid
graph TD
  H[Home data-view=home] -->|service or تحويل سريع| I[Input data-view=wizard]
  H -->|carousel eye| H
  I -->|validate wallet/to/amount + tafqit + fee 0| V{valid?}
  V -- no --> IERR[inline to/amount/balance errors]
  IERR --> I
  V -- yes --> RW[Review #proReviewOverlay]
  RW -->|cancel| I
  RW -->|ok| AU[Auth #proAuthOverlay bio or PIN]
  AU -->|POST transfer/exchange/pay| C{ok?}
  C -- no --> AUERR[toast failed, stay]
  AUERR --> AU
  C -- yes --> RC[Receipt #proReceiptOverlay copy/share/fav]
  RC -->|close| HIST[History + Recent refresh via /api/transactions]
  HIST --> H
```
Steps: select wallet (balance hint) → to (Yemen rule; exchange free-text; POS store field) → amount (tafqit words, over-balance block) → notes → fee `0 server only` → review masked name/phone → auth → receipt ref `BUQ-YYYY-######` → history. All demo `0-fee تجريبي`.
## F3 — Cashier sale (Login cashier → Session → Lookup → Sale → Receipt → Tx)
```mermaid
graph TD
  L[Login role=cashier + merchantBanner] -->|enterApp cashier| D[POS Dash data-cview=dash]
  D -->|open| S[Session open via POST /api/cashier/session]
  S --> LK[Lookup phone via GET /api/cashier/lookup]
  LK -- invalid --> LKERR[toast + stay]
  LK -- ok --> CHG[Charge enabled + customer card]
  CHG -->|POST /api/cashier/sale| R[Receipt in #posResult + session totals++]
  R --> TX[Tx data-cview=tx max 8]
  D -->|close| CLS[Session closed, totals kept]
  CLS --> D
```
Steps: open session → enter amount+phone → lookup masked customer → charge → receipt + totals — totals/fees **NEEDS-BACKEND-REVIEW**. Drawer/lang/sheets available throughout; `cgoto()` falls back to `dash` (never blank).