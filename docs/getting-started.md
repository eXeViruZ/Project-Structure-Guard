# Getting Started

## Installation

### From FAB (Marketplace)

1. Purchase and add **Project Structure Guard** to your project via FAB
2. Restart the Unreal Editor if prompted
3. Verify the plugin is enabled: **Edit → Plugins** → search for "Project Structure Guard"

### Manual Installation

1. Copy the `ProjectStructureGuard` folder into your project's `Plugins/` directory:
   ```
   YourProject/
     Plugins/
       ProjectStructureGuard/
         ProjectStructureGuard.uplugin
         Source/
         ...
   ```
2. Regenerate project files (right-click `.uproject` → **Generate Visual Studio project files**)
3. Build and launch the editor

---

## First Setup

### 1. Open Project Settings

**Edit → Project Settings → Project → Project Structure Guard**

You will see:

| Section | Purpose |
|---|---|
| **Naming Rules** | Define prefix, suffix, and casing requirements per asset class |
| **Folder Rules** | Define required folder paths per asset class |
| **Scan → Excluded Paths** | Paths to skip during scanning (e.g. `/Game/Developers`) |
| **Scan → Exclude Developer Folders** | Auto-skip developer content folders |
| **On-Save Validation** | Enable/disable real-time toast warnings on asset save |

### 2. Load a Preset

Instead of configuring rules manually, load a built-in preset:

1. Open the PSG window: **Window → Project Structure Guard**
2. Click one of the preset buttons at the top:
   - **Epic Official** — Follows Epic's naming conventions
   - **Allar Style Guide** — Community standard by Michael Allar
   - **Lyra** — Based on Epic's Lyra sample project

This populates your Naming Rules and Folder Rules automatically.

### 3. Run Your First Scan

1. In the PSG window, click the **Validation** tab
2. Click **Scan Whole Project**
3. Review the results:
   - **Errors** (red) — Must be fixed (e.g. missing prefix)
   - **Warnings** (yellow) — Should be fixed (e.g. wrong folder)
4. Use **Fix All Safe** to auto-rename, or **Move All Safe** to auto-relocate assets

---

## Project Settings Reference

### Naming Rules

Each naming rule has:

| Property | Description |
|---|---|
| **Asset Class Name** | Native class name to match (e.g. `StaticMesh`, `Blueprint`, `Material`). Empty = catch-all. |
| **Required Prefix** | Required prefix string (e.g. `SM_`, `BP_`, `M_`). Empty = no prefix check. |
| **Required Suffix** | Optional required suffix (e.g. `_D` for diffuse textures). Empty = no suffix check. |
| **Case Mode** | `Any`, `PascalCase`, `UPPERCASE`, or `lowercase` |
| **Severity** | `Error` or `Warning` |
| **Enabled** | Toggle rule on/off without deleting it |

> **Rule priority:** First matching rule (by Asset Class Name) wins. Place catch-all rules (empty class name) last.

### Folder Rules

Each folder rule has:

| Property | Description |
|---|---|
| **Asset Class Name** | Native class name to match. Empty = catch-all. |
| **Required Base Paths** | Array of paths the asset must be under (OR logic). e.g. `/Game/Art/Meshes` |
| **Severity** | `Error` or `Warning` |
| **Enabled** | Toggle rule on/off |

### Excluded Paths

Paths listed here are **completely skipped** during scanning. Default exclusions:

- `/Game/Developers` — Developer-only content
- `/Game/__ExternalActors__` — World Partition actors
- `/Game/__ExternalObjects__` — World Partition objects
- `/Game/_PSG_Quarantine` — Quarantined assets (always excluded automatically)

### On-Save Validation

When enabled, every asset save triggers a validation check. If a violation is detected, a **toast notification** appears with:

- The asset name and violation type
- A suggested fix (rename or move path)

Disable this if you prefer batch scanning only.
