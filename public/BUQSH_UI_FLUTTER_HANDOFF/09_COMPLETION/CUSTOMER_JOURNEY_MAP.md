# Customer Journey Map (FTU → Receipt/History/Profile)
Stages: Splash(1800ms) → Welcome → Onboarding(3) → Choose(#/chose_login_or_reg) → Login/Register(#authView/#regOverlay→OTP→PIN-setup) → Home(3x3 data-view=home) → Wallets(#walletDetails) → ServiceFlow(Input #proInputCard→Review→Auth→Processing→Receipt) → History/Notifications → Profile sub-views → Logout.
- Happy: demo 777000111/1234 → enterApp customer → carousel YER/SAR/USD → service → tafqit + fee 0 → masked review → PIN/bio → BUQ-YYYY-###### receipt → copy/share/fav → history refresh.
- Empty: no wallets → dashed + تغذية demo; no tx → لا نتائج + retry ↻; requested empty → لا طلبات.
- Error: phone/PIN inline + alert; over-balance block; API fail → toast failed + stay + retry; offline → skeleton then empty.
- Fallbacks: unknown goto → home + warn; Esc/scrim closes topmost; drawer nav closes then routes; hideBal persisted bq_hide; lang ar/en flips dir; demo badges kept.
- Guards: Yemen +967 9-digit start-7 (Arabic digits normalized), 4-digit PIN (0000 blocked), amount>0 ≤1e9 demo, exchange free-text only exception.