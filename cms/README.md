# vbwd-android-cms

A feature **plugin** for the [vbwd-android](https://github.com/vbwd-platform/vbwd-android-core)
plugin-host platform — the Kotlin · Jetpack Compose · Hilt port of the vbwd-ios
SDK. Plugin id: `cms` · version `0.1.0`.

Config-driven "Posts" browser over the host CMS embed archive.

## What it registers

Through the `PlatformSdk` facade (the single extension seam) this plugin contributes:
a route + menu item + translations — and registers nothing at all when its config keys are unset.

It touches **no core internals** — it depends on the public `:core` module only
(Open/Closed). Depends on **`:core`** only.

## Consume it

As a standalone module the plugin is published to GitHub Packages and consumed by
Maven coordinate:

```kotlin
// settings.gradle.kts — add the GitHub Packages repo (PAT with read:packages)
dependencyResolutionManagement {
    repositories {
        maven {
            url = uri("https://maven.pkg.github.com/vbwd-platform/vbwd-android-cms")
            credentials {
                username = System.getenv("GITHUB_ACTOR")
                password = System.getenv("GITHUB_TOKEN")
            }
        }
    }
}

// build.gradle.kts — register it in the host's available-plugins list
dependencies {
    implementation("com.vbwd:vbwd-android-cms:0.1.0")
}
```

Then add it to the host's `provideAvailablePlugins` list and to
`app/src/main/assets/plugins.json` (the enable/disable manifest).

## Build & test

```bash
./gradlew check        # ktlint + detekt + unit tests
```

## Docs

- [`docs/architecture.md`](docs/architecture.md) — how this plugin is wired.
- Original sprint report: `docs/dev_log/20260619/reports/09-A07-cms-plugin.md` in the umbrella repo.

## License

BSL 1.1 (Business Source License). Part of the **vbwd-platform** SDK.
