# Validation

The Validation tab is the primary interface for checking your project's asset naming and folder structure.

---

## Scanning

Open the PSG window (Tools → Project Structure Guard) and select the **Validation** tab.

Three scan modes are available:

| Button | Scope |
|---|---|
| **Scan Whole Project** | All assets under `/Game/` (excluding excluded paths) |
| **Scan Selected Folder** | Only the folder(s) selected in the Content Browser |
| **Scan Selected Assets** | Only the specific asset(s) selected in the Content Browser |

### Scan Results

After scanning, results appear in a sortable table:

| Column | Description |
|---|---|
| **Severity** | `Error` (red) or `Warning` (yellow) |
| **Asset** | Asset name |
| **Type** | `Naming` or `Folder` violation |
| **Description** | Human-readable description of the issue |
| **Suggested Fix** | Auto-generated fix (new name or target folder) |

Use the filter buttons to show/hide Errors, Warnings, or Auto-fixable only.

---

## Auto-Fix

### Rename (Naming Violations)

| Action | Description |
|---|---|
| **Fix Selected** | Rename only the selected assets in the list |
| **Fix All Safe** | Rename all assets that have a safe auto-fix suggestion |

A "safe" rename means PSG can deterministically compute the correct name (add prefix, remove wrong prefix, etc.). Ambiguous cases are skipped.

### Move (Folder Violations)

| Action | Description |
|---|---|
| **Move Selected** | Move only the selected assets to their suggested folder |
| **Move All Safe** | Move all assets with a clear target folder |

After moving assets, UE creates **redirectors**. Use the **Cleanup Redirectors** button to remove them.

---

## On-Save Validation

When enabled in Project Settings (`Enable On-Save Validation`), every `Ctrl+S` triggers an automatic check on the saved asset. If a violation is found, a toast notification appears:

```
[PSG] M_WrongPlace
[Folder] 'M_WrongPlace' is in '/Game/WrongFolder'.
Expected under: /Game/Art/Materials
Move to: /Game/Art/Materials
```

The toast is informational only — it does not block the save.

---

## Export Report (CSV)

Click **Export Report (CSV)** to save the current scan results as a `.csv` file in `Saved/PSGReports/`. The CSV includes:

```csv
# PSG Report - 2026.04.11-18.43.55
# Assets scanned: 20  |  Issues found: 5
# Errors: 4  |  Warnings: 1  |  Auto-fixable: 3

Severity,Asset,PackagePath,Type,Description,SuggestedFix,AutoFixable
Error,Ground_Dirty,/Game/Materials/Ground_Dirty,Naming,...,M_Ground_Dirty,Yes
```

---

## Cleanup Redirectors

After renaming or moving assets, UE leaves behind **Object Redirectors**. These ensure old references still work, but they clutter the Content Browser.

Click **Cleanup Redirectors** to find and fix up all redirectors in the project. This is equivalent to **Edit → Fix Up Redirectors in Folder** on the entire `/Game/` tree.
