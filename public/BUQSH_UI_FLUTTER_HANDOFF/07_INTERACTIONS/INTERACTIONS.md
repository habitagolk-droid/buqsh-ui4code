# 07 — Interactions (match web motion exactly in Flutter)
> Durations/easings below are from `styles.css`/`app.js`. Respect `prefers-reduced-motion` → instant (no anim) in Flutter via `MediaQuery.disableAnimations`.
| Component | Trigger / dismiss | Web anim | Flutter mapping |
|---|---|---|---|
| Card entrance | view show | `rise .45s ease (14px up + fade)` | `AnimatedOpacity+SlideTransition, Curves.easeOut, 450ms` |
| Role pill | tab tap | `transform 350ms cubic-bezier(.6,.1,.2,1.15)`, width=tab | `AnimatedPositioned` width+offset, same curve |
| Wallet carousel | swipe | `scroll-snap-x center`, dots 8→26px | `PageView(viewportFraction:.82) + DotsIndicator` |
| Promo (legacy) | auto 5s | dots + fade (currently minimal) | `Timer 5s` only if re-adding; otherwise omit |
| Drawer | menu / scrim / X / Esc / nav | `translateX(±105%→0) 320ms ease + scrim fade` | `Drawer` (RTL: `endDrawer`) or `Get` custom slide 320ms |
| Generic sheet | `openSheet()` / X / scrim / Esc | sheet `up .3s` from bottom, `r26 top`, `max-h 86vh` | `showModalBottomSheet(shape: R26 top, isScrollControlled)` |
| Pro Review/Auth/Receipt | continue/ok/confirm / X / Esc | `.pro-sheet up .3s`, scrim `.6` | `Get.bottomSheet(barrier .6, rounded 24 top)` |
| Register sheet | `أنشئ حساباً` / X / scrim / Esc | same pro-sheet | same as above |
| Toast | any `toast()` | pill fade+`translateY 20→0` 300ms, hold 2600ms | `Get.snackbar(snackPosition: BOTTOM, 2600ms)` styled dark pill |
| PIN dots | input | bar `.on` dark 250ms | `AnimatedContainer 250ms` ×4 |
| Bio scan | tap | text `...` 5×320ms → `✓` green | staged `Future.delayed` + haptic-light equiv (no real auth) |
| Skeleton | fetch start | `shimmer bg-pos 1.2s infinite` | `Shimmer.fromColors` same period |
| Success | API ok | green alert + `ok-ic` 56px `#1F7A33` | green container + check 56 |
| Spinner | submit | 22px border-spin `.8s linear` | `CircularProgressIndicator(strokeWidth 3)` lime/dark |
| Header wave | static | svg 30px `fill bg` | `CustomPainter` wave 30px |
| Focus ring | input focus | border brand + `0 0 0 4px lime .6` | `FocusNode` border + outer glow container |
| Haptics | none on web | N/A (visual only) | optional `HapticFeedback.lightImpact` on CTA success only |
Dismiss rules: scrim-tap closes (except auth during `proDoConfirm` loading — keep open, disable confirm); Esc closes topmost; drawer nav also closes drawer then `goto()` (never blank).