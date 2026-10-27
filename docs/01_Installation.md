# 01 - Installation and Updating

> **v1.3.0 release preparation.** PSG v1.2.0 remains publicly available on Fab until the new version is approved and live.

## Engine and Platform Requirements

- **v1.3.0 (pending)** and **v1.2.0 (public)**: Unreal Engine **5.8**, editor-only C++ plugin.
- **v1.1.1**: the earlier Unreal Engine **5.7** compatible release.
- Descriptor platforms: **Win64, Mac and Linux**. The v1.3 package has been built on Win64; this documentation does not certify native Mac/Linux builds.
- The v1.3 **Adopt Project > Create Initial Baseline** write path requires a supported local Windows physical filesystem. It is restricted on Mac/Linux or unsupported sandbox/network filesystem paths.
- No runtime gameplay component is required for packaged games.

## Install through Fab

1. Open **Project Structure Guard** in your Fab library or the [Fab listing](https://www.fab.com/listings/7dfc5ec6-1261-4f86-8e69-82ea0ae1e8a2).
2. In Epic Games Launcher, locate the Fab Library entry and choose the package compatible with your installed Unreal Engine.
3. Install to the desired engine and start Unreal Editor.
4. Open **Edit > Plugins**, enable **Project Structure Guard**, and restart if prompted.

Do not expect the v1.3 package to be available until Fab finishes publishing the submitted version.

## Manual Installation

1. Extract the provided plugin package.
2. Place the folder containing `ProjectStructureGuard.uplugin` into exactly one of:
   - `[YourProject]/Plugins/ProjectStructureGuard/`, or
   - `[UnrealEngine]/Engine/Plugins/ProjectStructureGuard/`.
3. Avoid duplicate engine-wide and project-local PSG installations, or mixed previous/new versions on Unreal plugin search paths.
4. If using a source-only archive, allow Unreal Engine to compile the plugin for your host as required.
5. Start the editor, enable PSG and restart when requested.

## Open PSG

In Unreal Editor choose **Tools > Project Structure Guard**. The plugin provides **Validation**, **Unused Assets**, **Rules**, **Inspector**, **Policy Diagnostics** and **Adopt Project** tabs.

## Upgrade from v1.2.0 to v1.3.0

No asset-content migration is part of the documented v1.3 update. However, the release adds policy and baseline workflows, so review settings rather than assuming old and new policy configurations are interchangeable.

1. Commit or back up your project and the active PSG settings and baseline JSON.
2. Close Unreal Editor and remove/replace the **old plugin install only**. Do not delete project settings or baselines.
3. Install the correct UE 5.8 package and reopen the project.
4. Open **Project Settings > Project Structure Guard**. Check global naming/folder rules, excluded/protected paths, any Scoped Policies, the configured baseline path, and the CI Default Profile.
5. Run **Scan Whole Project** and inspect the **Baseline Review** and **Policy Diagnostics** results.
6. Use **Inspector** to review effective policies in representative folders before performing rename/move/cleanup operations.
7. If adopting a previously untracked project, use **Adopt Project**. Existing baselines are **not** overwritten by Create Initial Baseline or the normal Create Baseline control.
8. If existing CI jobs use legacy `-failon...` flags, they retain the legacy behavior unless you deliberately add `-profile=...`.

Do not delete historical baseline JSONs or quarantine data as part of an ordinary plugin update. If a baseline changes unexpectedly, investigate the path/identity before selecting any write action.

## Further Reading

- [Getting Started](02_Getting_Started.md)
- [Scoped Policies and Inspector](10_Policies_Inspector_Diagnostics.md)
- [Baseline Review and Adoption](11_Baselines_Adoption.md)
- [Troubleshooting](08_Troubleshooting.md)
