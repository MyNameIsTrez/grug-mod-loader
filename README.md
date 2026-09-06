# grug for Minecraft

[grug](https://github.com/grug-lang/grug)'s primary goal is to serve as a faithful digital preservation format for mods, so that players can continue enjoying the hard work of mod authors for decades to come.

https://github.com/user-attachments/assets/2a7949ae-643c-4274-9a06-12e528affe97

In the video above, four different Minecraft environments all hot-reload the same grug file:
* Minecraft 1.20.6 with Forge
* Minecraft Beta 1.7.3 with Ornithe
* Minecraft Beta 1.7.3 with StationAPI
* Minecraft Alpha 1.1.2_01 with Ornithe

> [!NOTE]
> `mod_api.json` is currently frozen. We will not be expanding the API until comprehensive test coverage and Continuous Integration (CI) pipelines are fully established. Once expansion resumes, new API additions will initially be limited to features Minecraft Alpha supports, so that mods stay compatible across every supported version from Alpha onward.

## Licensing

If a mod contains copyrighted material or prohibits redistribution, please [open a GitHub issue](https://github.com/grug-lang/grug-for-minecraft/issues) with supporting evidence.

[`mods/examplemod`](mods/examplemod) is the reference mod that tutorials and other mods are meant to copy from. It's licensed under the [BSD Zero Clause License](https://opensource.org/license/0bsd), the license grug recommends for all mods written from scratch, so that snippets and files can be copied between mods as freely as possible.

## Long-term Plans

This repository aims to become a thoroughly vetted, centralized host for grug mods via the `mods/` directory at its root, rather than depending on external platforms like Modrinth or CurseForge. Support for downloading mods through APIs like Modrinth's may be added eventually, but isn't a priority given the `mods/` directory already covers hosting, discovery, and vetting on its own. Because `mod_api.json` restricts what mods can do, CI will be able to auto-merge pull requests that only modify grug code and come from a GitHub account listed as an author in the mod's `about.json`, while reviewers focus on resource files.

An in-game mod portal will let players browse, install, and update mods without restarting the game, get notified of new releases and changelogs, and even write new mods from scratch using a built-in text editor and Scratch-like blocks interface. Since `mod_api.json` specifies which versions of the game each function is available in (Minecraft Alpha, for example, didn't have a hunger system), the portal will also be able to disable grug files that call functions unavailable in the current version, using `e""` entity strings to detect when disabling one file cascades into disabling others that depend on it. Keeping mods centralized in this repository also means the portal can give players a way to freely copy-paste and search real-world grug code across every mod, whether to learn from it or reuse it in their own.

## For Players

In the future, `grug-for-minecraft` will ship ready-to-use releases that work out-of-the-box on Windows, macOS, and Linux.

## For Developers

### Requirements

If you are developing or building `grug-for-minecraft` from source, your system must have the following tools installed and available on your system `PATH`:

*   **Java Development Kit (JDK) 21**: Required to compile the mod loaders (specifically Forge 1.20.6 requires Java 21).
*   **Git**: Used by the Gradle script to clone and fetch the `grug-rs` repository.
*   **Rust**: Required to compile [grug-rs](https://github.com/grug-lang/grug-rs) into a static library.
*   **Python 3**: Required to execute `generate.py`, which auto-generates the C JNI bindings and Java bridge files.
*   **C Compiler**: Required to compile the generated C code and the Rust static library into the final native shared library.

### Running from Source

Use the following Gradle commands to build and run the specific mod loader environments:

| Minecraft Version | Mod Loader | Command |
| :--- | :--- | :--- |
| **1.20.6** | Forge | `./gradlew :loaders:1.20.6-forge:runClient` |
| **Beta 1.7.3** | Ornithe | `./gradlew :loaders:b1.7.3-ornithe:runClient` |
| **Beta 1.7.3** | StationAPI | `./gradlew :loaders:b1.7.3-stationapi:runClient` |
| **Alpha 1.1.2_01** | Ornithe | `./gradlew :loaders:a1.1.2_01-ornithe:runClient` |
