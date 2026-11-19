# 05 — Source Manifest (frozen pointer, no code duplication)
> Do NOT copy code into this folder. Reference canonical files below. UI is frozen; edit only via normal web release, never from handoff docs.
## Canonical sources
| File | Role | How to inspect |
|---|---|---|
| `public/index.html` | DOM + ids + i18n keys + nav/drawer/sheets skeleton | View source; ids `ftu*`, `authView`, `customerApp/cashierApp`, `pro*Overlay`, `sideDrawer`, `sheetOverlay` |
| `public/styles.css` | All tokens/classes (`:root`, header, card, wallet, nav, drawer, sheet, FTU) | Copy values into `ThemeData`; see `03_DESIGN_SYSTEM` |
| `public/app.js` | State + validation + router + fetch + masking/tafqit/i18n | Mirror `state`, `validatePhone/PIN`, `goto/cgoto`, `openSheet/openPro`, `tafqit/mask*` in Dart |
| `worker/index.js` | Mock API contracts (demo) | Base for Dart `ApiClient`; confirm schemas with backend |
Snapshot (approx, verify with `wc -c`): `index.html` ~15–20KB, `styles.css` ~12–16KB, `app.js` ~35–45KB, `worker/index.js` ~8–12KB.
## Copy instructions for Flutter devs
1. Read `BUQSH_UI_HANDOFF_MASTER.md` + `02_*_SPECS` before opening code.
2. Open the four files read-only; do not run codemods from here.
3. Port screens 1:1 per `02` + tokens per `03` + motion per `07`.
4. Keep `demo` badges/texts; flag divergences as **NEEDS-BACKEND-REVIEW**.
## API endpoint list (demo mocks — confirm with backend)
- `POST /api/login {phone, pin, role}` → `{ok, token, user}`
- `POST /api/register {name, phone, pin}` → `{ok, token, user}`
- `GET /api/health`, `GET /api/wallets`, `GET /api/transactions`
- `POST /api/transfer|request|deposit|withdraw|exchange|pay {wallet,to,amount,notes,store}` → `{ok, operationNumber, timestamp, fee:0}`
- `GET /api/notifications`
- `GET|POST /api/cashier/session`, `GET /api/cashier/lookup?phone=`, `POST /api/cashier/sale {phone,amount}`