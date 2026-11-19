# Remaining Screens Catalog — S00-S18 CONFIRMED + R01-R30 New (Docs-only)
> Frozen brand #0C4A40 / #278D5B / #D4E157, Cairo RTL. Demo 777000111 / 1234. Fees/limits NEEDS-BACKEND-REVIEW.
## S00-S18 CONFIRMED (do not redesign)
S00 splash #ftuSplash • S01 welcome #ftuWelcome • S02 onboarding #ftuOnboard • S03 choose #chose_login_or_reg • S04 login #authView + register #regOverlay • S05 home data-view=home (3x3) • S06 wallets data-view=wallets • S07 wizard-input #proInputCard • S08 review #proReviewOverlay • S09 auth #proAuthOverlay • S10 receipt #proReceiptOverlay • S11 history • S12 notifications • S13 profile • S14 qr • S15 pos-dash data-cview=dash • S16 pos-tx data-cview=tx • S17 drawer #sideDrawer • S18 sheets #sheetOverlay + toast.
## New R screens (implemented HTML/CSS/JS demo)
| ID | Arabic | Anchor | Dart suggestion | Status |
|---|---|---|---|---|
| R01 | تحقق OTP | #otpOverlay | modules/auth/otp_view | DEMO |
| R02 | معلومات التسجيل | #regStepInfo | modules/auth/signup_info_view | DEMO |
| R03 | إعداد PIN | #regStepPin | modules/auth/pin_setup_view | DEMO |
| R04 | نسيت PIN | #forgotOverlay | modules/auth/forgot_view | DEMO |
| R05 | إعادة تعيين PIN | #resetOverlay | modules/auth/reset_view | DEMO |
| R06 | تحقق الكاميرا | #cameraOverlay | modules/auth/camera_view | DEMO |
| R07 | توثيق KYC | #kycOverlay | modules/auth/kyc_view | DEMO |
| R08 | تفاصيل المحفظة | data-view=wallets #walletDetails | modules/customer/wallet_details_view | DEMO |
| R09 | تحويل بين محافظ | wizard svc=transfer | modules/customer/wallet_transfer_view | DEMO |
| R10 | مصارفة | wizard svc=exchange | modules/customer/exchange_view | DEMO |
| R11 | تفاصيل عملية | data-view=txdetails | modules/customer/tx_details_view | DEMO |
| R12 | مشاركة إيصال | shareReceipt | widgets/share_sheet | DEMO |
| R13 | المطلوبة قائمة | data-view=requested | modules/customer/requested_list_view | DEMO |
| R14 | المطلوبة تفاصيل | sheet receipt | modules/customer/requested_details_view | DEMO |
| R15 | سحب نقدي | wizard svc=transfer(cashout) | modules/customer/cashout_view | DEMO |
| R16 | تغذية | wizard svc=deposit | modules/customer/add_money_view | DEMO |
| R17 | دفع POS عميل | wizard svc=pos + store | modules/customer/pos_pay_view | DEMO |
| R18 | إيصال POS | #posResult/#proReceiptOverlay | modules/customer/pos_receipt_view | DEMO |
| R19 | تعديل الملف | sheet epName | modules/profile/edit_profile_view | DEMO |
| R20 | تغيير PIN | sheet cpPin | modules/profile/change_pin_view | DEMO |
| R21 | تغيير اللغة | goto language | modules/profile/language_view | CONFIRMED |
| R22 | حدود المعاملات | data-view=limits /api/limits | modules/profile/limits_view | DEMO + NEEDS-BACKEND-REVIEW |
| R23 | FAQ/دعم/شروط/خصوصية/عن | openInfoSheet | modules/profile/info_views | DEMO |
| R24 | مشاركة QR | #qrShareOverlay | modules/profile/qr_share_view | DEMO |
| R25 | دخول كاشير | #authView cashier | modules/cashier/login_view | CONFIRMED |
| R26 | رمز تأكيد كاشير | #cashierCodeOverlay | modules/cashier/code_view | DEMO |
| R27 | محافظ كاشير | data-cview=wallets | modules/cashier/wallets_view | DEMO |
| R28 | ملف كاشير | data-cview=profile | modules/cashier/profile_view | DEMO |
| R29 | استرداد | data-cview=refund /api/cashier/refund | modules/cashier/refund_view | DEMO + NEEDS-BACKEND-REVIEW |
| R30 | بيع/فواتير خدمات POS | data-cview=dash | modules/cashier/sale_view | DEMO |
Shared: login-card/pro-sheet/tx-card/set-row/bottom-nav/drawer/toast. Phone +967 Yemen 9-digit start-7, PIN 4-digit, fee 0 server-only.