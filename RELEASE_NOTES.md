# Release Notes

## 0.3.0

Public API cleanup. Clean break from 0.2.1 (no shipped consumers, no back-compat shims).

- Participant-scoped methods no longer take a `participantId` argument. The SDK now decodes the participantId from the stored participant JWT and fills the URL path internally, so `(participantToken, participantId)` can no longer drift out of sync. Affected: `getParticipant`, `updateParticipant`, `getParticipantReferrals`, `getParticipantRewards`, `sendInvites`, `updateVanityLinks`, `getParticipantCommissions`, `markParticipantCommissionsRead`, `getParticipantPayouts`, `markParticipantPayoutsRead`, `getParticipantAffiliateSummary`, `getParticipantReferralSummary`, `requestPaypalConfirmEmail`, `markParticipantRewardsRead`, `trackShare`, `triggerReferral`.
- Adds `suspend fun getCurrentParticipantId(): String?` (plus a `GrowSurfCallback<String?>` overload) returning the participantId from the stored participant JWT, or `null` if none.
- Removes the public `createParticipant(...)` method and its callback overload; use `addParticipant(...)`.
- Removes the `updateParticipant(input: GrowSurfParticipantInput)` convenience overload; use the `GrowSurfParticipantUpdateInput` form.
- Collapses `updateVanityLink` + `updateVanityLinks` into a single `updateVanityLinks(vanityKeys: List<String>)`.
- `createSession()` (and its callback overload) is now `internal`; the SDK manages the campaign session itself. `recordAttribution(...)` is public so host apps can report attributions captured outside the built-in deep-link / deferred flows.
- Adds an `X-GRSF-SDK-VERSION` request header (sourced from a single SDK version constant) alongside the existing platform header.
- Adds `fun close()` (and folds the same teardown into `shutdown()`) to cancel the SDK's internal callback scope.
- Raises `minSdk` to 24 and the Java/Kotlin bytecode target to 17.
- `onParticipantCreated` in `GrowSurfWindowCallbacks` is now `(GrowSurfParticipant, String?) -> Unit`, passing the new participant token alongside the participant.
- The four in-memory store classes (`MemoryGrowSurf*`) are now `internal`. Protocols and production defaults stay public.
- Server contract is unchanged; URL paths still carry `:participantId`, now filled locally from the JWT.
- `POST /session` now includes the device's `mobileInstanceId` in the request body so the server can scope the session rate limit per device instead of per IP. Multiple devices behind one NAT (office Wi-Fi, dev box + emulator + phone, CGNAT carrier) no longer share a single bucket. The SDK also retries `/session` once after a 1.5 s delay on a 429 response so a single hairline trip is absorbed silently instead of surfacing the raw rate-limit message in the GrowSurf window UI. Older servers that don't read `mobileInstanceId` ignore the field and continue per-IP limiting.


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
