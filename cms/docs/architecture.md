# vbwd-android-cms — architecture

Port of the iOS `cms` plugin. Plugin id `cms`,
version `0.1.0`.

## Boundary

This module depends on **`:core` only**. The
build's `dependencyBoundaryCheck` task enforces that boundary; an undeclared
edge to another plugin (or to `:app`) fails the build. The plugin is a thin
**composition root**: `Plugin.install(sdk)` wires the domain (services/stores),
the Compose views, and the menu items — each in its own file (Single
Responsibility).

## Extension seams used

Config-driven "Posts" browser over the host CMS embed archive.

Concretely it registers: a route + menu item + translations — and registers nothing at all when its config keys are unset — all via the `PlatformSdk` facade, never by
reaching into a registry or the host's composition root (Interface Segregation /
Dependency Inversion).

## Lifecycle

`install` (register seams) → `activate` (mark live) → `deactivate` / `uninstall`
(tear down — unsubscribe events, release stores). A failure in any hook is
**isolated** by the host's `PluginRegistry`: this plugin becomes
`PluginStatus.Error` without aborting its peers.

## See also

- The plugin contract: `Plugin` / `PlatformSdk` / `PluginHost` in `vbwd-android-core`.
- The full sprint write-up: `docs/dev_log/20260619/reports/09-A07-cms-plugin.md` (umbrella repo).
