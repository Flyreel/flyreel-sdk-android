# Flyreel SDK

[![Platform](https://img.shields.io/badge/platform-Android-orange.svg)](https://github.com/Flyreel/flyreel-sdk-android)
[![Languages](https://img.shields.io/badge/language-Kotlin-orange.svg)](https://github.com/Flyreel/flyreel-sdk-android)
[![GitHub release](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://flyreelsdk.jfrog.io/artifactory/flyreel-androidsdk)

## Requirements:

Minimum Android SDK version - `23`

## Installation

1. Add Flyreel maven repository to your project's `settings.gradle.kts` file:

```kotlin
dependencyResolutionManagement {
    // ...
    repositories {
        // ...
        maven("https://flyreelsdk.jfrog.io/artifactory/flyreel-androidsdk")
    }
}
```

2. Add the following dependency to your app's `build.gradle.kts` file:

```kotlin
dependencies {
    // ...
    implementation("lexisnexis.flyreel:android-sdk:1.0.0")
}
```

<details>
<summary>Legacy</summary>

1. Add Flyreel maven repository to your project's `build.gradle` file:

```groovy
allprojects {
    repositories {
        // ...
        maven {
            url "https://flyreelsdk.jfrog.io/artifactory/flyreel-androidsdk"
        }
    }
}
```

2. Add the following dependency to your app's `build.gradle` file:

```groovy
dependencies {
    // ...
    implementation 'lexisnexis.flyreel:android-sdk:1.0.0'
}

```

</details>

## Usage

### Initialization

To use the Flyreel SDK, you must provide a configuration with the following parameters:

`settingsVersion`: Identifier of your remote SDK settings.

`organizationId`: Identifier of your organization.

Then you need to call `Flyreel.initalize()` method in your Application's onCreate() method. (Don't
forget to register your application class in AndroidManifest.xml)

```kotlin
class MyApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        val configuration = FlyreelConfiguration(
            organizationId = "7d3899f1421a7650241516475",
            settingsVersion = 1,
        )
        Flyreel.initialize(
            application = this,
            configuration = configuration
        )
    }

}
```

> **_NOTE:_** Setting up the configuration is mandatory. Attempting to open the SDK flow without it
> will result in a fatal error.

### How to open Flyreel chat

Invoke openFlyreel() method with a context

```kotlin
Flyreel.openFlyreel(context = requireContext())
```

### Deep Linking

If you're launching the Flyreel flow from a deep link, push notification, or a custom solution where
user details can be provided automatically, use:

```kotlin

fun openFlyreel(
    context: Context,
    zipCode: String,
    accessCode: String,
    shouldSkipLoginPage: Boolean = true
)

fun openFlyreel(
    context: Context,
    deeplinkUri: Uri? = null,
    shouldSkipLoginPage: Boolean = true
)
```

## Debug Logs

Enable debug logging for troubleshooting purposes:

```kotlin
Flyreel.enableLogs()
````

## Sandbox

Verify your implementation in the sandbox mode. Initialize Flyreel with an additional parameter:

```kotlin
val configuration = FlyreelConfiguration(
    organizationId = "7d3899f1421a7650241516475",
    settingsVersion = 1,
    environment = FlyreelEnvironment.Sandbox
)

Flyreel.initialize(
    application = this,
    configuration = configuration
)
```
