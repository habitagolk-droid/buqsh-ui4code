# Screen → Route Traceability (S00-S18 + R01-R30)
| Screen ID | Arabic name | Service | Web Active Route | Dart File | Controller | Repository | Screenshot | Status |
|---|---|---|---|---|---|---|---|---|
| S00 | البداية | FTU | overlay #ftuSplash | ftu/splash_view | SplashController | — | S00-splash-ar.png | CONFIRMED |
| S01 | ترحيب | FTU | #ftuWelcome | ftu/welcome_view | FtuController | — | S01-welcome-ar.png | CONFIRMED |
| S02 | تعريف | FTU | #ftuOnboard | ftu/onboarding_view | FtuController | — | S02-onboarding-ar.png | CONFIRMED |
| S03 | اختيار | FTU | #/chose_login_or_reg | ftu/choose_view | FtuController | — | S03-choose-ar.png | CONFIRMED |
| S04 | دخول/تسجيل | auth | #/login #authView/#regOverlay | auth/login_view | AuthController | AuthRepository /api/login /api/register | S04-login-ar.png | CONFIRMED |
| S05 | الرئيسية | home 3x3 | data-view=home | customer/home_view | HomeController | WalletRepository /api/wallets | S05-home-ar.png | CONFIRMED |
| S06 | محافظي | wallets | data-view=wallets | customer/wallets_view | WalletController | WalletRepository | S06-wallets-ar.png | CONFIRMED |
| S07 | إدخال | service | data-view=wizard #proInputCard | customer/wizard_input_view | WizardController | TransferRepository | S07-input-ar.png | CONFIRMED |
| S08 | مراجعة | service | #proReviewOverlay | customer/review_sheet | WizardController | — | S08-review-ar.png | CONFIRMED |
| S09 | توثيق | service | #proAuthOverlay | customer/auth_sheet | WizardController | — | S09-auth-ar.png | CONFIRMED |
| S10 | إيصال | service | #proReceiptOverlay | customer/receipt_sheet | WizardController | — | S10-receipt-ar.png | CONFIRMED |
| S11 | السجل | history | data-view=history | customer/history_view | TxController | TxRepository /api/transactions | S11-history-ar.png | CONFIRMED |
| S12 | تنبيهات | notif | data-view=notifications | customer/notifications_view | NotifController | /api/notifications | S12-notif-ar.png | CONFIRMED |
| S13 | حسابي | profile | data-view=profile | customer/profile_view | ProfileController | /api/profile | S13-profile-ar.png | CONFIRMED |
| S14 | مسح QR | qr | data-view=qr | customer/qr_view | QrController | — | S14-qr-ar.png | DEMO |
| S15 | مبيعات | POS | data-cview=dash | cashier/pos_dash_view | SessionController | CashierRepository /api/cashier/* | S15-pos-ar.png | CONFIRMED |
| S16 | عمليات التاجر | POS | data-cview=tx | cashier/pos_tx_view | SessionController | CashierRepository | S16-postx-ar.png | CONFIRMED |
| S17 | الدرج | nav | #sideDrawer | widgets/drawer | NavController | — | S17-drawer-ar.png | CONFIRMED |
| S18 | شيت/توست | global | #sheetOverlay #toast | widgets/sheet+toast | UiController | — | S18-sheet-ar.png | CONFIRMED |
| R01 | تحقق OTP | auth | #otpOverlay /api/otp/* | auth/otp_view | AuthController | AuthRepository | R01-otp-ar.png | DEMO |
| R02 | معلومات التسجيل | auth | #regStepInfo | auth/signup_info_view | AuthController | AuthRepository | R02-signup-ar.png | DEMO |
| R03 | إعداد PIN | auth | #regStepPin | auth/pin_setup_view | AuthController | AuthRepository | R03-pinsetup-ar.png | DEMO |
| R04 | نسيت PIN | auth | #forgotOverlay /api/pin/forgot | auth/forgot_view | AuthController | AuthRepository | R04-forgot-ar.png | DEMO |
| R05 | إعادة PIN | auth | #resetOverlay /api/pin/reset | auth/reset_view | AuthController | AuthRepository | R05-reset-ar.png | DEMO |
| R06 | كاميرا | auth | #cameraOverlay | auth/camera_view | KycController | — | R06-camera-ar.png | DEMO |
| R07 | KYC | auth | #kycOverlay | auth/kyc_view | KycController | — | R07-kyc-ar.png | DEMO |
| R08 | تفاصيل محفظة | wallets | data-view=wallets #walletDetails | customer/wallet_details_view | WalletController | WalletRepository | R08-wdetails-ar.png | DEMO |
| R11 | تفاصيل عملية | tx | data-view=txdetails | customer/tx_details_view | TxController | TxRepository | R11-txdetails-ar.png | DEMO |
| R13 | المطلوبة | request | data-view=requested /api/requested | customer/requested_list_view | TxController | TxRepository | R13-requested-ar.png | DEMO |
| R22 | الحدود | profile | data-view=limits /api/limits | profile/limits_view | ProfileController | ProfileRepository | R22-limits-ar.png | NEEDS-BACKEND-REVIEW |
| R24 | مشاركة QR | profile | #qrShareOverlay | profile/qr_share_view | ProfileController | — | R24-qrshare-ar.png | DEMO |
| R26 | رمز الكاشير | cashier | #cashierCodeOverlay | cashier/code_view | SessionController | CashierRepository | R26-ccode-ar.png | DEMO |
| R27 | محافظ الكاشير | cashier | data-cview=wallets | cashier/wallets_view | SessionController | CashierRepository | R27-cwallets-ar.png | DEMO |
| R29 | استرداد | cashier | data-cview=refund /api/cashier/refund | cashier/refund_view | SessionController | CashierRepository | R29-refund-ar.png | NEEDS-BACKEND-REVIEW |
| UNKNOWN | أسعار/رسوم حقيقية | — | — | — | — | — | — | NOT-IMPLEMENTED |
Legend: CONFIRMED=frozen web exists; DEMO=mock UI ok; NEEDS-BACKEND-REVIEW=confirm server; UNKNOWN=honestly unknown.