# GrowSurf Android SDK Distribution

Public distribution metadata for the GrowSurf Android SDK. The SDK implementation source is private; Android customers install compiled artifacts from Maven Central.

## Installation

Add Maven Central and the core SDK dependency.

### Kotlin DSL

```kotlin
repositories {
    mavenCentral()
}

dependencies {
    implementation("com.growsurf:growsurf-android-sdk:0.3.2")
}
```

### Groovy

```groovy
repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.growsurf:growsurf-android-sdk:0.3.2'
}
```

Optional attribution adapters are published separately. They do not bundle vendor SDKs; your app still owns Branch, Adjust, AppsFlyer, or Singular setup.

### Kotlin DSL

```kotlin
dependencies {
    implementation("com.growsurf:growsurf-android-sdk-attribution-branch:0.3.2")
    implementation("com.growsurf:growsurf-android-sdk-attribution-adjust:0.3.2")
    implementation("com.growsurf:growsurf-android-sdk-attribution-appsflyer:0.3.2")
    implementation("com.growsurf:growsurf-android-sdk-attribution-singular:0.3.2")
}
```

### Groovy

```groovy
dependencies {
    implementation 'com.growsurf:growsurf-android-sdk-attribution-branch:0.3.2'
    implementation 'com.growsurf:growsurf-android-sdk-attribution-adjust:0.3.2'
    implementation 'com.growsurf:growsurf-android-sdk-attribution-appsflyer:0.3.2'
    implementation 'com.growsurf:growsurf-android-sdk-attribution-singular:0.3.2'
}
```

Manual AAR installation is a fallback only. Maven Central is the recommended install path because Gradle resolves transitive dependencies automatically.

## Maven Coordinates

- `com.growsurf:growsurf-android-sdk:0.3.2`
- `com.growsurf:growsurf-android-sdk-attribution-branch:0.3.2`
- `com.growsurf:growsurf-android-sdk-attribution-adjust:0.3.2`
- `com.growsurf:growsurf-android-sdk-attribution-appsflyer:0.3.2`
- `com.growsurf:growsurf-android-sdk-attribution-singular:0.3.2`

## Documentation

See the public Android SDK docs:

```text
https://docs.growsurf.com/developer-tools/android-sdk
```
