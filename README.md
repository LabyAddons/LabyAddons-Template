# LabyMod Addon Template

A clean and ready-to-use **LabyMod Addon Template** for building your own LabyMod addons with Gradle and the official LabyMod Gradle plugins.

Whether you're creating your first addon or starting a larger project, this template provides a structured foundation with everything you need to get started quickly.

## ✨ Features

* 🧩 Multi-module Gradle project
* 🎮 LabyMod development environment
* ⚙️ Example addon with configuration
* 💬 Example commands and subcommands
* 🌍 Internationalization support
* 🚀 GitHub Actions CI workflow
* 🛠️ Gradle Wrapper included
* 📦 Ready-to-customize addon structure

---

## 📋 Quick Overview

| Property         | Value                             |
| ---------------- | --------------------------------- |
| **Group**        | `de.jardateien`                   |
| **Namespace**    | `example`                         |
| **Display Name** | `ExampleAddon`                    |
| **Author**       | `JarDateien`                      |
| **Java**         | 21                                |
| **Main Class**   | `de.jardateien.core.ExampleAddon` |

---

## 📦 Project Structure

```text
.
├── api/
│   └── src/
│       └── main/
│
├── core/
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   │   └── de/jardateien/core/
│       │   │       ├── ExampleAddon.java
│       │   │       ├── ExampleConfiguration.java
│       │   │       └── commands/
│       │   │
│       │   └── resources/
│       │       └── assets/
│       │           └── example/
│       │               └── i18n/
│       │                   └── en_us.json
│
├── game-runner/
│
├── gradle/
├── build.gradle.kts
├── gradle.properties
├── gradlew
├── gradlew.bat
└── settings.gradle.kts
```

### Modules

**`api/`**
Contains API-related classes and interfaces used by the addon.

**`core/`**
The main addon module containing the actual addon implementation, configuration, commands and resources.

**`game-runner/`**
Provides the configuration required to run Minecraft in the development environment.

---

## 🔧 Prerequisites

Before getting started, make sure you have:

* **JDK 21**
* **Git**
* An internet connection for downloading dependencies
* A compatible IDE such as IntelliJ IDEA

The project already includes the **Gradle Wrapper**, so you do not need to install Gradle manually.

---

## 🚀 Getting Started

Clone the repository and enter the project directory:

```bash
git clone https://github.com/LabyAddons/LabyAddons-Template.git
cd LabyAddons-Template
```

You can then import the project into your preferred Java IDE.

---

## 🏗️ Build

Build the complete project from the repository root:

### Linux / macOS

```bash
./gradlew build
```

### Windows

```bat
gradlew.bat build
```

To build only the core module:

```bash
./gradlew :core:build
```

The project uses the included Gradle Wrapper and the official LabyMod Gradle plugin.

Minecraft versions used by the development environment are configured through:

```text
gradle.properties
```

---

## 🎮 Development Environment

The template already contains a configured Minecraft client run.

To see all available Gradle tasks:

```bash
./gradlew tasks
```

Depending on the generated LabyMod Gradle tasks, the development client can usually be started with:

```bash
./gradlew runClient
```

The exact task name may vary depending on the configured Minecraft version and LabyMod Gradle plugin version.

### Development Login

If required, you can enable the development login for the configured client run:

```kotlin
runs {
    getByName("client") {
        devLogin = true
    }
}
```

This can be found inside the `labyMod` Minecraft run configuration in `build.gradle.kts`.

---

## 💬 Example Commands

The template includes a small example command implementation.

### `/ping`

Displays:

```text
Ping!
```

### `/ping pong`

Displays:

```text
Ping Pong!
```

The example also demonstrates how aliases and subcommands can be registered.

Relevant files:

```text
core/src/main/java/de/jardateien/core/commands/
```

---

## ⚙️ Customization

Before using the template for your own addon, update the following values.

### Package

Change the project group and default package in:

```text
build.gradle.kts
```

For example:

```kotlin
group = "com.example"
```

and:

```kotlin
defaultPackageName = "com.example.myaddon"
```

Make sure to move your Java/Kotlin source files so that the directory structure matches the new package.

---

### Addon Information

Update the addon metadata inside the `labyMod.addonInfo` block:

```kotlin
labyMod {
    addonInfo {
        namespace = "myaddon"
        displayName = "MyAddon"
        author = "YourName"
        description = "Your addon description"
        minecraftVersion = "*"
    }
}
```

#### Important properties

| Property           | Description                     |
| ------------------ | ------------------------------- |
| `namespace`        | Unique identifier of your addon |
| `displayName`      | Name displayed to users         |
| `author`           | Author or organization          |
| `description`      | Short addon description         |
| `minecraftVersion` | Supported Minecraft version(s)  |

---

## 🌍 Internationalization

Translations are stored inside:

```text
core/src/main/resources/assets/<namespace>/i18n/
```

For example:

```text
core/src/main/resources/assets/example/i18n/en_us.json
```

You can add additional languages by creating the corresponding locale files.

For example:

```text
en_us.json
de_de.json
fr_fr.json
```

When changing your addon namespace, make sure to update the corresponding resource directory as well.

---

## 📚 Dependencies

Additional dependencies can be added in:

```text
core/build.gradle.kts
```

For example:

```kotlin
dependencies {
    implementation("group:artifact:version")
}
```

Only add dependencies that are actually required by your addon.

---

## 🤖 GitHub Actions

The template includes a GitHub Actions workflow:

```text
.github/workflows/build.yml
```

The workflow automatically builds the project when changes are pushed or pull requests are created.

You can extend the workflow with additional steps such as:

* Automated tests
* Artifact uploads
* Release builds
* Publishing
* Additional code checks

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Verify that the project builds successfully.
5. Open a Pull Request with a description of your changes.

Before submitting a Pull Request, make sure the project still builds successfully:

```bash
./gradlew build
```

---

## 📄 License

This project is licensed under the **LabyAddons Community License**.

The license allows you to use, modify, fork, distribute and commercially use the project, provided that the required attribution remains.

See the [`LICENSE`](LICENSE) file for the complete license terms.

---

## ❤️ LabyAddons

This template is maintained as part of **LabyAddons** and is intended to make starting with LabyMod addon development easier.

**Created by [LabyAddons](https://github.com/LabyAddons)**
