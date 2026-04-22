# 07 — CI/CD Commandlet

## Overview

Project Structure Guard ships with a headless commandlet that runs validation without opening the Unreal Editor UI.

This allows you to integrate PSG into CI/CD pipelines (GitHub Actions, Jenkins, TeamCity, etc.) and fail builds automatically when violations are detected.

---

## Basic Usage

```bash
UnrealEditor.exe "[YourProject].uproject" -run=PSGValidate
```

---

## All Options

| Flag | Description |
|------|-------------|
| `-outputjson=<path>` | Write JSON report to the specified file path |
| `-outputcsv=<path>` | Write CSV report to the specified file path |
| `-failonerror` | Exit with code 1 if any Error-severity issues are found |
| `-failonwarning` | Exit with code 1 if any issues are found (errors + warnings) |
| `-scanpath=<path>` | Scan only assets under this package path (default: `/Game`) |
| `-quiet` | Suppress per-issue log output |

---

## Exit Codes

| Code | Meaning |
|------|---------|
| `0` | No issues found (or only warnings without `-failonwarning`) |
| `1` | Issues found (with `-failonerror` or `-failonwarning`) |
| `2` | Internal error |

---

## Examples

**Basic scan, fail on errors:**
```bash
UnrealEditor.exe "MyGame.uproject" -run=PSGValidate -failonerror
```

**Export JSON report, scan subfolder only:**
```bash
UnrealEditor.exe "MyGame.uproject" -run=PSGValidate \
  -outputjson="Reports/psg_report.json" \
  -scanpath=/Game/Characters
```

**Full CI run — JSON + CSV, fail on any issue, quiet log:**
```bash
UnrealEditor.exe "MyGame.uproject" -run=PSGValidate \
  -outputjson="Reports/psg.json" \
  -outputcsv="Reports/psg.csv" \
  -failonwarning \
  -quiet
```

---

## CSV Report Format

Columns:

```
Severity, Asset, PackagePath, Type, Description, SuggestedFix, AutoFixable
```

Output path when no `-outputcsv` is specified:

```
[ProjectDir]/Saved/PSGReports/PSG_Report_YYYYMMDD_HHMMSS.csv
```

---

## GitHub Actions Example

```yaml
- name: Run PSG Validation
  run: |
    "$UE_PATH/UnrealEditor.exe" "$PROJECT" \
      -run=PSGValidate \
      -outputjson=psg_report.json \
      -failonerror \
      -quiet

- name: Upload PSG Report
  uses: actions/upload-artifact@v3
  with:
    name: psg-report
    path: psg_report.json
```
