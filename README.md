# LabyMod Addon Template

A minimal LabyMod addon template to get you started building LabyMod addons with Gradle and the official LabyMod Gradle plugins.

This repository provides:
- A multi-module Gradle project (api, core, game-runner) configured for LabyMod development.
- A working example addon implementation (core) with configuration, commands and a listener.
- Gradle wrapper and a GitHub Actions workflow for CI.

---

## Quick overview

- Group: `de.jardateien` (see root Gradle configuration)
- Example addon namespace: `example`
- Display name: `ExampleAddon`
- Author: `JarDateien`
- Java compatibility: Java 21 (set in subprojects)
- Where the main addon lives: `core/src/main/java/de/jardateien/core/ExampleAddon.java`

---

## Prerequisites

- JDK 21
- Git
- Network access to resolve dependencies
- Gradle wrapper is included; you can use `./gradlew` (Unix/macOS) or `gradlew.bat` (Windows)

---

## Build

From the repository root:

- Build everything:
  - Unix/macOS: `./gradlew build`
  - Windows: `gradlew.bat build`

- Build only the core module:
  - `./gradlew :core:build`

The project uses the included Gradle wrapper and the LabyMod Gradle plugin. Minecraft versions used for runs are read from the Gradle property `net.labymod.minecraft-versions` (see `gradle.properties`).

---

## Development / Run in dev environment

The Gradle config already registers a `client` run — the project uses the LabyMod Gradle plugin to configure Minecraft runs. To start a development client, use the run task provided by the plugin (task name depends on plugin-generated tasks; commonly something like `runClient` or a custom run configured as `client`). Example (replace with the actual run task name if different):

- `./gradlew runClient` (or check `./gradlew tasks` for the exact run task)

In the build script you can enable dev login for the client run by uncommenting or setting `devLogin = true` in the `labyMod { minecraft { ... runs { getByName("client") { devLogin = true } } } }` block.

---

## Project structure

- `api/` — API module where annotation-processor and API-only interfaces live.
  - `api/build.gradle.kts` configures annotation processor/reference type.
- `core/` — Main addon implementation (contains the example addon).
  - `core/src/main/java/org/example/core/ExampleAddon.java` — addon entry point (annotated with `@AddonMain`).
  - `core/src/main/java/org/example/core/ExampleConfiguration.java` — example configuration class (with a boolean enabled property).
  - `core/src/main/java/org/example/core/commands/` — example chat command (`ping` and subcommand `pong`).
  - `core/src/main/resources/assets/example/i18n/en_us.json` — example localization file.
- `game-runner/` — helper module for running the game in specific configurations (contains `gradle.properties` for runs).
- `gradle/`, `gradlew`, `gradlew.bat` — Gradle wrapper and tooling.
- `.github/workflows/build.yml` — GitHub Actions workflow to build the project on push/PR.

---

## Example usage (commands)

The example addon registers a simple chat command:

- `/ping` → displays `Ping!` (uses color AQUA)
- `/pong` (alias/sub-command) → displays `Ping Pong!` (GRAY)
- Using the alias registered (`"pong"`) will display `Pong!` as the main command's alternate response.

(See `core/src/main/java/de/jardateien/core/commands/ExamplePingCommand.java` and `ExamplePingSubCommand.java`.)

---

## Customization

Before publishing your addon, make these common edits:

- Change the group and package names:
  - Edit `group` in `build.gradle.kts` (root) and update `defaultPackageName` to your package (e.g., `com.myname.addon`).
  - Move Java/Kotlin sources to match the new package path (update directory structure under `core/src/main/java`).

- Update addon metadata (in `build.gradle.kts` root `labyMod.addonInfo` block):
  - `namespace` — unique addon id (used for assets/namespace).
  - `displayName` — visible name for your addon.
  - `author` — author name(s).
  - `description` — short description shown in UIs.
  - `minecraftVersion` — restrict to a Minecraft version or leave `*` for all.

- Add dependencies used by your addon in `core/build.gradle.kts` (example of adding external maven dependency is included as a commented line).

---

## Internationalization and assets

- Locale files live under:
  - `core/src/main/resources/assets/<namespace>/i18n/`
  - Example: `core/src/main/resources/assets/example/i18n/en_us.json`

- Replace `example` namespace and update translations as needed.

---

## CI

A GitHub Actions workflow is provided at `.github/workflows/build.yml` to build the project on push and pull requests. Adjust the workflow if you need publishing steps or additional checks.

---

## Contributing

1. Fork the repo and create a feature branch.
2. Make changes, ensure they compile: `./gradlew build`.
3. Open a Pull Request describing your changes.
4. Add tests or examples when appropriate.

If you'd like a contribution guide or issue templates, add them under `.github/`.

---

## License

No license file is included in this template. Add a `LICENSE` (for example MIT, Apache-2.0) to indicate how others may use your code.

---

If you want, I can:
- Generate a ready-to-commit README.md file with this content.
- Add a basic LICENSE (MIT / Apache-2.0) and a CONTRIBUTING.md template.
