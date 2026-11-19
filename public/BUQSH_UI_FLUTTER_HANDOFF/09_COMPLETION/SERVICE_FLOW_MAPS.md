# Service Flow Maps — 9 Independent Flows (Input-Review-Auth-Receipt pattern)
> Fee 0 server-only. No invented pricing. Endpoints: /api/deposit|transfer|request|withdraw|exchange|pay.
## 1) تغذية Add-Money (deposit)
```mermaid
graph TD
A[Entry: home تغذية / walletDetails تغذية]-->B[Input wizard wallet+amount+notes]
B-->C{valid? balance n/a}
C--no-->B
C--yes-->D[Review masked + fee 0]
D-->E[Auth PIN/bio]
E-->F[POST /api/deposit]
F-->G[Receipt BUQ + share/fav]
G-->H[History refresh + back/retry]
```
## 2) حوالة محلية Send (transfer)
```mermaid
graph TD
A[Entry: حوالة / تحويل سريع]-->B[Input wallet+to Yemen+amount+tafqit]
B-->C{phone+amount valid?}
C--no-->B
C--yes-->D[SelectionSheets fav/contacts/scan]
D-->E[Review]
E-->F[Auth]
F-->G[POST /api/transfer]
G-->H[Receipt]
```
## 3) تحويل بين محافظ Internal (request)
```mermaid
graph TD
A[Entry: تحويلات]-->B[Input wallet+to+amount]
B-->C{valid?}
C--yes-->D[Review]
D-->E[Auth]
E-->F[POST /api/request]
F-->G[Receipt + history]
```
## 4) مصارفة Exchange
```mermaid
graph TD
A[Entry: شبكي]-->B[Input wallet+free to+amount]
B-->C{amount>0? no Yemen rule}
C--yes-->D[Review]
D-->E[Auth]
E-->F[POST /api/exchange]
F-->G[Receipt]
```
## 5) إلكتروني E-pay
```mermaid
graph TD
A[Entry: إلكتروني / QR scan demo]-->B[Input wallet+to+amount]
B-->C[Review]
C-->D[Auth]
D-->E[POST /api/pay]
E-->F[Receipt]
```
## 6) نقاط بيع POS (customer)
```mermaid
graph TD
A[Entry: POS / store strip]-->B[Input wallet+to+store+amount]
B-->C{store required demo}
C--yes-->D[Review + store row]
D-->E[Auth]
E-->F[POST /api/pay + store]
F-->G[POS Receipt + share]
```
## 7) سحب نقدي Cash-Out
```mermaid
graph TD
A[Entry: سحب]-->B[Input wallet+agent phone+amount]
B-->C{over-balance block}
C--yes-->D[Review]
D-->E[Auth]
E-->F[POST /api/transfer agent]
F-->G[Receipt + code demo]
```
## 8) فواتير Bills
```mermaid
graph TD
A[Entry: فواتير]-->B[Input wallet+biller+invoice+amount]
B-->C[Review]
C-->D[Auth]
D-->E[POST /api/pay]
E-->F[Receipt]
```
## 9) ألعاب/شبكي Games
```mermaid
graph TD
A[Entry: ألعاب]-->B[Input wallet+account+amount]
B-->C[Review]
C-->D[Auth]
D-->E[POST /api/pay]
E-->F[Receipt]
```
Common states: Processing spinner #proProcessing, Success green receipt, Failure red + Retry (stay on auth/input), Back closes overlay, Empty skeleton/dashed, Offline toast failed + retry.