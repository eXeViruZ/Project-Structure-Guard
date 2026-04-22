# 05 — Rule Manager

## Rules Tab

The **Rules** tab in the PSG window gives you direct control over which rules are active without opening Project Settings.

It shows two lists:
- **Naming Rules**
- **Folder Rules**

Each row displays:

| Column | Description |
|--------|-------------|
| Enabled | Checkbox — toggle the rule on or off |
| Asset Class | The class this rule applies to |
| Description | Prefix/suffix or required folder path |
| Severity | Error or Warning |

Changes are saved immediately and take effect on the next scan.

---

## Built-in Presets

PSG ships with three ready-to-use rule sets:

| Preset | Based on |
|--------|----------|
| **Epic Official** | Unreal Engine official asset naming conventions |
| **Allar Style Guide** | Gamemakin UE Style Guide by Allar |
| **Lyra Sample Project** | Naming conventions used in Epic's Lyra project |

Load a preset via the **Presets** menu in the PSG toolbar.

> Loading a preset replaces all current naming and folder rules. Your previous rules are not backed up automatically — export them first if needed.

---

## Rule Export

1. Click **Export Rules** in the PSG toolbar.
2. Choose a save location.
3. PSG writes a human-readable JSON file containing all current naming and folder rules.

The JSON file is suitable for version control and team sharing.

---

## Rule Import

1. Click **Import Rules** in the PSG toolbar.
2. Select a previously exported JSON file.
3. PSG replaces the current rules with the imported set.
4. The Rules tab refreshes automatically.

---

## JSON Format

Example naming rule entry:

```json
{
  "AssetClass": "StaticMesh",
  "RequiredPrefix": "SM_",
  "RequiredSuffix": "",
  "Severity": "Error",
  "bEnabled": true
}
```

Example folder rule entry:

```json
{
  "AssetClass": "StaticMesh",
  "RequiredFolder": "/Game/Meshes",
  "Severity": "Warning",
  "bEnabled": true
}
```
