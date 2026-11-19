# 05 — Service Flow Maps (9 services + detailed Transfer + SmartAuth)
> Endpoints: `deposit→/api/deposit`, `transfer→/api/transfer`, `request→/api/request`, `pay_elec|pos|bills|games→/api/pay`, `withdraw→/api/transfer(agent demo)`, `exchange→/api/exchange`. Fee `0` server-only. Store field only for `pos`. Yemen phone rule except `exchange` (free text). Demo `777000111/1234`.
## Deposit — تغذية `/api/deposit`
```mermaid
graph TD
A[Home تغذية]-->B[Input wallet+amount+notes]
B-->C{amount>0?}
C--no-->B
C--yes-->D[Review fee 0]
D-->E[SmartAuth]
E-->F[POST /api/deposit]
F-->G[Receipt BUQ copy/share/fav]
```
## Transfer — حوالة `/api/transfer` (DETAILED 4-STAGE)
```mermaid
graph TD
A[Entry: حوالة / تحويل سريع / walletDetails تحويل]-->B[Input: wallet select + to Yemen + amount + tafqit + notes]
B-->C{validatePro? phone 9-digit start-7 + amount>0 + balance ok}
C--no-->BERR[inline to/amount/balance errors + Continue disabled]
BERR-->B
C--yes-->D[Review: masked Name *** + ****0111 demo + wallet + fee 0 + non-cancellable warn]
D-->|cancel/X|B
D-->|ok|E{SmartAuth XOR}
E-->|bio supported|EB[Bio tap 1200ms -> server wait]
E-->|no bio|EP[PIN 4 demo 1234 -> confirm]
EB-->|fail/cancel|FB[fallback: back or use-PIN, NO execute]
FB-->EP
EB-->|success|F[POST /api/transfer + wait]
EP-->F
F--fail-->FERR[toast failed + stay + retry, bio-success invalidated]
FERR-->E
F--ok-->G[Receipt BUQ-YYYY-###### + share/fav + history refresh]
```
### SmartAuth decision
```mermaid
graph TD
S[openAuth]-->R[renderProAuthSmart: bio? XOR pin]
R-->|bio|T[tap #proBioBtn -> processing -> success Must wait server]
R-->|pin|P[enter 4 -> confirm enabled -> proDoConfirm false]
T-->|cancel/fail|Q[showPinFallback: back-to-review OR switch-to-pin]
Q-->P
T-->|ok|W[proDoConfirm true -> POST -> Receipt]
P-->W
```
## Request — تحويلات `/api/request`
```mermaid
graph TD
A[Home تحويلات]-->B[Input wallet+to+amount]
B-->C{valid?}
C--yes-->D[Review]
D-->E[Auth]
E-->F[POST /api/request]
F-->G[Receipt]
```
## Pay_elec — إلكتروني `/api/pay`
```mermaid
graph TD
A[Home إلكتروني / QR scan BUQ-SCAN-DEMO]-->B[Input wallet+to+amount]
B-->C[Review]
C-->D[Auth]
D-->E[POST /api/pay]
E-->F[Receipt]
```
## POS — نقاط بيع `/api/pay + store`
```mermaid
graph TD
A[Home POS / stores strip]-->B[Input wallet+to+store required+amount]
B-->C{store+phone+amount?}
C--yes-->D[Review + store row]
D-->E[Auth]
E-->F[POST /api/pay store]
F-->G[POS Receipt + share]
```
## Withdraw — سحب `/api/transfer agent`
```mermaid
graph TD
A[Home سحب]-->B[Input wallet+agent phone+amount]
B-->C{over-balance block}
C--yes-->D[Review]
D-->E[Auth]
E-->F[POST agent]
F-->G[Receipt + code demo]
```
## Bills — فواتير `/api/pay`
```mermaid
graph TD
A[Home فواتير]-->B[Input wallet+biller+invoice+amount]
B-->C[Review]
C-->D[Auth]
D-->E[POST /api/pay]
E-->F[Receipt]
```
## Games — ألعاب `/api/pay`
```mermaid
graph TD
A[Home ألعاب]-->B[Input wallet+account+amount]
B-->C[Review]
C-->D[Auth]
D-->E[POST /api/pay]
E-->F[Receipt]
```
## Exchange — شبكي `/api/exchange`
```mermaid
graph TD
A[Home شبكي]-->B[Input wallet+free-text to+amount, no Yemen rule]
B-->C{amount>0?}
C--yes-->D[Review]
D-->E[Auth]
E-->F[POST /api/exchange]
F-->G[Receipt]