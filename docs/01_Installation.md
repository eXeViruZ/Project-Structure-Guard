# 01 — Installation

## Requirements

For the current release line:

- **Project Structure Guard v1.2.0**
- **Unreal Engine 5.8**
- Windows, Mac, or Linux
- Editor-only — no runtime gameplay dependency

> Unreal Engine 5.7 remains supported through the earlier **v1.1.1** release. Do not install the v1.2.0 package into UE 5.7.

---

## Install from Fab

1. Purchase or open **Project Structure Guard** in your Fab library.
2. Open the Epic Games Launcher.
3. Go to **Library → Fab Library**.
4. Find **Project Structure Guard**.
5. Install the version that matches your Unreal Engine installation:
   - **v1.2.0 for UE 5.8**
   - **v1.1.1 for UE 5.7**

---

## Install Manually (ZIP)

1. Download the plugin package for your Unreal Engine version.
2. Extract the ZIP. You will get a `ProjectStructureGuard` plugin folder.
3. Copy that folder into one of the following locations:
   - **Engine-wide:** `[UE Install]/Engine/Plugins/ProjectStructureGuard/`
   - **Project-only:** `[YourProject]/Plugins/ProjectStructureGuard/`
4. Restart the Unreal Editor.

Do not keep two different Project Structure Guard versions installed in locations that Unreal can load at the same time.

---

## Enable the Plugin

1. Open your project in Unreal Editor.
2. Go to **Edit → Plugins**.
3. Search for **Project Structure Guard**.
4. Enable the plugin.
5. Restart the editor if prompted.

---

## Open the Tool

After restart, open the tool via:

```text
Tools → Project Structure Guard
```

The Project Structure Guard window can be docked into the Unreal Editor layout.

---

## Updating from an Earlier Version

Updating to Project Structure Guard v1.2.0 does **not** require asset migration.

Before updating an active production project, it is still recommended to:

1. Commit or back up your project configuration.
2. Close the Unreal Editor.
3. Replace the older plugin installation with the UE 5.8 v1.2.0 package.
4. Reopen the project and confirm the plugin loads normally.
5. Review your Project Structure Guard settings, rules, protected paths, and baseline configuration before running structural fixes.

Project rules and baseline data can be kept in source control when stored in project-relative locations.
