# Missing Screens Report — Counts + Screenshots + Backend Flags
## Counts
- Existing frozen S00-S18: 19 entries — all CONFIRMED (S14 QR demo-only by design).
- Newly completed R01-R30: 30 screens implemented (HTML/CSS/JS + demo APIs).
- Remaining NOT-IMPLEMENTED: 0 functional screens; only UNKNOWN real pricing/fees (intentionally not invented).
## Screenshot coverage (actual, see ACTUAL_SCREENSHOTS/README)
- Required: S00-S18 AR + R-key screens AR (min 25 files) + EN mirrors for login/home/wizard/review/receipt (5 files) = ~30 PNGs, 480px, demo badges visible.
- Inventory tracked in traceability Screenshot column (S00-splash-ar.png … R29-refund-ar.png); missing file = capture pending, never claimed as done.
## Demo warnings
> تجريبي — demo • 0 fees (server only) • 256-bit display only. No real money. Public demo 777000111 / 1234; 0000 rejected; OTP demo 1234; camera/KYC/QR-scan simulated.
## Backend-review flags
| Item | Web today | Action |
|---|---|---|
| Fees | always 0 | confirm real table per rail/currency |
| Limits | /api/limits demo | confirm min/max/daily/monthly |
| OTP | 1234 fixed | real SMS + expiry + attempts |
| KYC/camera | placeholder | real review flow |
| Session totals | in-memory | authoritative source |
| Schemas | BUQ-YYYY-###### mock | freeze OpenAPI + errors AR/EN |
## Separation / identity preserved
3x3 home (9 only), CUSTOMER vs CASHIER fully separated, #0C4A40/#278D5B/#D4E157 + Cairo RTL unchanged, S00-S18 untouched, +967 Yemen + 4-digit PIN rules kept.