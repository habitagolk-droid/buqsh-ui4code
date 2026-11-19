# BUQSH UI4Code — Independent UI Workspace

This repository contains the original BUQSH interactive web prototype and its Flutter/GetX handoff documentation.

## Scope
- UI prototype source: `public/index.html`, `public/styles.css`, `public/app.js`
- Prototype worker: `worker/index.js` (demo only; not the production BUQSH API)
- Flutter handoff documentation: `public/BUQSH_UI_FLUTTER_HANDOFF/`
- Flutter-ready registry/specifications: `public/BUQSH_UI2CODE_FLUTTER_READY/`

## Safety rules
1. This is a separate UI workspace. It must not replace or modify `habitagolk-droid/buqsh`.
2. The Flutter repository remains the runtime source of truth.
3. Treat demo users, balances, transactions, credentials, fees, limits, security claims, and Hono worker responses as illustrative only.
4. Preserve BUQSH identity, RTL/Arabic-first behavior, existing features, and separate customer/cashier flows.
5. Do not port mock API behavior into production Flutter/backend without independent verification.

## Run the web prototype
The source archive uses Bun and Hono/Cloudflare Workers tooling. See `package.json`, `README.md`, and `wrangler.jsonc` for the original commands and configuration.

## Starting point
Read `public/BUQSH_UI_HANDOFF_MASTER.md`, then `public/BUQSH_UI2CODE_FLUTTER_READY/README.md` and `public/BUQSH_UI2CODE_FLUTTER_READY/01_DESIGN_VS_PROTOTYPE_VS_SOURCE_VS_FLUTTER.md`.
