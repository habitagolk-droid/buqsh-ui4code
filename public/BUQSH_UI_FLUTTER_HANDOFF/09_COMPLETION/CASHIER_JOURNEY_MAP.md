# Cashier Journey Map (separated from Customer)
Stages: Login(role=cashier + merchantBanner) → Code(#cashierCodeOverlay demo 1234) → Home Dash(data-cview=dash) → Session open/close(POST /api/cashier/session) → Lookup(GET /api/cashier/lookup masked ****) → Sale(amount+phone→POST /api/cashier/sale fee 0) → Receipt(#posResult BUQ + session totals++) → Tx(data-cview=tx max8) → Wallets(data-cview=wallets) → Profile(data-cview=profile) → Refund(data-cview=refund POST /api/cashier/refund) → Logout(clears bq_session → choose).
- Session: open resets totals demo; close keeps totals; totals NEEDS-BACKEND-REVIEW (in-memory mock).
- PII: displayName *** + masked ****last4 only; phone validated Yemen rule.
- Errors: invalid phone/amount toast + stay; sale fail toast failed + retry; cgoto unknown → dash fallback (never blank).
- Separation: #customerApp hidden when cashier; separate bottom-nav 5 tabs (sales/tx/wallets/refund/profile); no shared wallet mutation.