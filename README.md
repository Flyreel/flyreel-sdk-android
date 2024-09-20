# Flyreel SDK

[![Platform](https://img.shields.io/badge/platform-Android-green.svg)](https://github.com/Flyreel/flyreel-sdk-android)
[![Languages](https://img.shields.io/badge/language-Kotlin-orange.svg)](https://github.com/Flyreel/flyreel-sdk-android)
[![jFrog release](https://img.shields.io/maven-metadata/v?metadataUrl=https%3A%2F%2Fflyreelsdk.jfrog.io%2Fartifactory%2Fflyreel-androidsdk%2Flexisnexis%2Fflyreel%2Fandroid-sdk%2Fmaven-metadata.xml&label=jfrog)](https://flyreelsdk.jfrog.io/artifactory/flyreel-androidsdk)

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
    implementation("lexisnexis.flyreel:android-sdk:$flyreelVersion")
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
    implementation "lexisnexis.flyreel:android-sdk:$flyreelVersion"
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

### Custom fonts

If you want to use custom fonts in the Flyreel chat, you have two options:

- add your font **ttf** file to the assets folder
- add your font **ttf** file to the res/font folder

Then, you can use the font's name in the dashboard panel.
For example, if you have added font **my_font.ttf** to the assets folder, you can use **my_font** as
a font name in the Flyreel dashboard.

## Debug Logs

Enable debug logging for troubleshooting purposes:

```kotlin
Flyreel.enableLogs()
```

## Flyreel status check
You can manually check Flyreel status

```kotlin
///This function makes a network request to retrieve the status of Flyreel for the specified zip code and access code
fun fetchFlyreelStatus(zipCode: String, accessCode: String, onSuccess: (FlyreelStatus) -> Unit, onError: (FlyreelError) -> Unit)
```

## Analytics

```kotlin
/// Subscribes to a stream of analytic events and handles each event with a provided callback.
///
/// This function observes a feed of analytic events from the SDK. When an event
/// is received, the provided handler callback is called with the event as its argument.
///
/// - Parameters:
///   - handler: A callback that is called with the analytic event emitted by the SDK.
///     The callback takes a single parameter:
///       - event: A `FlyreelAnalyticEvent` type that contains event's data.
Flyreel.observeAnalyticEvents { event ->
    YourAnalyticProvider.send(event)
}
```

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
