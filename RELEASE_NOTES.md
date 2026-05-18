# Release Notes

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
