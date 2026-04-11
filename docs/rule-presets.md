# Rule Presets

Project Structure Guard ships with three built-in rule presets and supports custom rule sharing via JSON files.

---

## Built-in Presets

Load a preset from the **Validation** tab by clicking one of the preset buttons:

### Epic Official

Based on Epic Games' internal naming conventions. Includes rules for:

| Asset Type | Prefix | Example |
|---|---|---|
| Blueprint | `BP_` | `BP_PlayerCharacter` |
| Material | `M_` | `M_Ground` |
| Material Instance | `MI_` | `MI_Ground_Inst` |
| Static Mesh | `SM_` | `SM_Rock` |
| Skeletal Mesh | `SK_` | `SK_Character` |
| Texture | `T_` | `T_Ground_D` |
| Widget Blueprint | `WBP_` | `WBP_MainMenu` |
| Animation Blueprint | `ABP_` | `ABP_Character` |
| Animation Montage | `AM_` | `AM_Attack` |
| Particle System | `PS_` | `PS_Fire` |
| Sound Cue | `SC_` | `SC_Footstep` |
| Sound Wave | `SW_` | `SW_Explosion` |
| ... and more | | |

### Allar Style Guide

Based on the widely-adopted [Allar UE5 Style Guide](https://github.com/Allar/ue5-style-guide). Similar to Epic but with some variations in prefix conventions.

### Lyra

Based on Epic's Lyra sample project. Includes rules tailored to Lyra's specific folder and naming patterns.

---

## Loading a Preset

> **Warning:** Loading a preset **replaces** your current naming and folder rules. Export your current rules first if you want to keep them.

1. Open the PSG window → **Validation** tab
2. Click **Epic Official**, **Allar Style Guide**, or **Lyra**
3. Rules are applied immediately

---

## Custom Rules

You can add, modify, or delete rules in **Project Settings → Project Structure Guard**.

### Adding a Naming Rule

1. Go to **Naming Rules** → click the **+** button
2. Fill in:
   - **Asset Class Name:** e.g. `NiagaraSystem`
   - **Required Prefix:** e.g. `NS_`
   - **Severity:** `Error` or `Warning`
3. Save settings

### Adding a Folder Rule

1. Go to **Folder Rules** → click the **+** button
2. Fill in:
   - **Asset Class Name:** e.g. `Material`
   - **Required Base Paths:** e.g. `/Game/Art/Materials`
   - **Severity:** `Warning`
3. Save settings

---

## Export / Import Rules (JSON)

Share rules across team members or projects using JSON files.

### Export

1. In the PSG window, click **Export Rules** (top right)
2. A JSON file is saved and its path is shown in a notification
3. Share this file with your team via source control, Slack, email, etc.

### Import

1. Click **Import Rules** (top right)
2. Select a `.json` file
3. Rules from the file are **merged** into your current settings

The JSON file contains all naming and folder rules in a portable format that works across any project using Project Structure Guard.

---

## Rule Priority

- **Naming rules** are evaluated top-to-bottom. The **first matching rule** (by Asset Class Name) wins.
- Place **specific rules** (e.g. `StaticMesh`) above **catch-all rules** (empty Asset Class Name).
- Disabled rules are skipped entirely.
