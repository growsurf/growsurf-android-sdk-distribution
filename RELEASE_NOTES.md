# Release Notes

## 0.2.1

Security hardening for the native GrowSurf window cache and the in-window image loader.

- Encrypts the window cache via `EncryptedSharedPreferences` (AES-256-GCM values, AES-256-SIV keys, MasterKey-wrapped) so participant data no longer sits in plaintext `SharedPreferences`. Legacy `growsurf_window_cache` entries are cleared on first use.
- Re-validates every redirect hop in the in-window remote image loader against the supported scheme allow-list and propagates an `https`-required flag through the chain to block `https → http` downgrade attempts.
- No public API or installation changes. Source-compatible upgrade from 0.2.0.

## 0.2.0

Adds the native GrowSurf window beta and expands attribution adapter coverage.

- Adds `com.growsurf:growsurf-android-sdk-attribution-singular:0.2.0`.
- Adds native GrowSurf window support for sharing, invites, referrals, rewards, leaderboard, affiliate summary, commissions, payouts, participant settings, FAQ, how-it-works, and terms sections.
- Keeps participant sharing centered on the canonical `shareUrl`.
- Publishes the core SDK and optional Branch, Adjust, AppsFlyer, and Singular adapter artifacts to Maven Central.

The release workflow creates a Central Portal user-managed deployment. Release the deployment in Central Portal after validation passes before announcing the Maven coordinates broadly.

## 0.1.0

Initial public release of the GrowSurf Android SDK on Maven Central.

- Defines the Maven Central coordinates for the core Android SDK.
- Defines optional Branch, Adjust, and AppsFlyer attribution adapter coordinates.
- Documents Kotlin DSL and Groovy Gradle installation snippets.
- Keeps implementation source private while pointing public metadata at this distribution repository.
