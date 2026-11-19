# 01 — Screenshots Capture Guide (text-only, no binaries committed)
This folder intentionally contains NO png/jpg. Capture locally and name per convention below.
## Screen list (IDs must match file names)
| File | Screen ID | What must be visible |
|---|---|---|
| `00_splash_{ar,en}.png` | splash `#ftuSplash` | logo circle ب + BUQSH بقش + loader |
| `01_welcome_{ar,en}.png` | welcome `#ftuWelcome` | kicker/title/sub + wallet scene + استمرار + تخطي |
| `02_onboarding_{ar,en}.png` | onboarding `#ftuOnboard` | 3 slides + dots + السابق/التالي + ابدأ الآن on last |
| `03_choose_{ar,en}.png` | choose `#chose_login_or_reg` | login + create-account buttons + demo hint |
| `04_login_customer_{ar,en}.png` | login customer | role pill عميل + phone + PIN dots + demo buttons + bio |
| `05_login_cashier_{ar,en}.png` | login cashier | merchant banner + same form, role=كاشير |
| `06_register_{ar,en}.png` | register `#regOverlay` | name/phone/PIN + إنشاء الحساب |
| `07_home_{ar,en}.png` | home | pro-header + wallet carousel + 3×3 services + recent + stores |
| `08_wallets_{ar,en}.png` | wallets | wallet detail cards YER/SAR/USD |
| `09_wizard_input_{ar,en}.png` | wizard input | wallet select + to + amount + tafqit + fee 0 |
| `10_review_{ar,en}.png` | review sheet | amount card + to/wallet/fee rows |
| `11_auth_{ar,en}.png` | auth sheet | fingerprint + PIN |
| `12_receipt_{ar,en}.png` | receipt sheet | ref copy + share + fav |
| `13_history_{ar,en}.png` | history | chips + search + tx cards |
| `14_notifications_{ar,en}.png` | notifications | list + read button |
| `15_profile_{ar,en}.png` | profile | hero avatar + name + phone |
| `16_qr_{ar,en}.png` | qr | scanner frame + scan demo |
| `17_pos_dash_{ar,en}.png` | pos dash | session card + lookup + charge |
| `18_pos_tx_{ar,en}.png` | pos tx | cashier tx list |
| `19_drawer_{ar,en}.png` | drawer | open drawer RTL + active row |
| `20_states_{ar,en}.png` | states | loading skeleton + error alert + empty |
## Capture checklist (high-clarity, uncropped)
1. Viewport 480px width (`.app-shell max-width:480px`), device pixel ratio 2–3, light theme only.
2. Capture BOTH `ar (rtl)` and `en (ltr)` via lang toggle; keep `dir` attribute correct.
3. Hide devtools/cursor; no cropping — include header + card + bottom-nav + footer where present.
4. Include sheets fully expanded (review/auth/receipt/register/generic) + scrim.
5. Include each state: loading (spinner/skeleton shimmer), success (green alert/check), error (red alert + field red border), empty (dashed box).
6. Keep `demo` badges, `0 fees`, `256-bit`, `demo: 777000111 / 1234` visible — do not blur.
7. Desktop: also capture ≥1024px to show `side-brand` panel; mobile: 360px to verify `row2/row3` stack.
8. Name exactly `NN_name_{ar|en}.png`; place in this folder locally (git-ignored if needed). Do not embed binaries in MD.