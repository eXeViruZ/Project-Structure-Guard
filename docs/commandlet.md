# Commandlet (CI/CD Integration)

Project Structure Guard includes a commandlet for headless validation. Run it from the command line in CI/CD pipelines, pre-commit hooks, or automated build scripts.

---

## Basic Usage

```bash
"<EnginePath>/UnrealEditor-Cmd.exe" "<ProjectPath>.uproject" -run=PSGValidate -stdout -unattended
```

### Example

```bash
"E:\UE_5.7\Engine\Binaries\Win64\UnrealEditor-Cmd.exe" "G:\MyProject\MyProject.uproject" -run=PSGValidate -stdout -unattended
```

---

## Command-Line Arguments

| Argument | Description | Default |
|---|---|---|
| `-scanpath=/Game` | Root path to scan | `/Game` |
| `-failonerror` | Exit code 1 if any **errors** are found | Off |
| `-failonwarning` | Exit code 1 if any **issues** (errors or warnings) are found | Off |
| `-quiet` | Suppress individual issue lines in the log (summary only) | Off |
| `-outputjson="path.json"` | Write a JSON report to the specified path | None |
| `-outputcsv="path.csv"` | Write a CSV report to the specified path | None |

If neither `-outputjson` nor `-outputcsv` is specified, a default CSV report is written to `Saved/PSGReports/`.

---

## Exit Codes

| Code | Meaning |
|---|---|
| `0` | PASSED — no issues, or issues found but no fail flag set |
| `1` | FAILED — issues found and `-failonerror` or `-failonwarning` is set |
| `2` | ERROR — settings could not be loaded |

---

## Log Output

```
LogPSGCommandlet: ===================================================
LogPSGCommandlet:   Project Structure Guard - Commandlet Validation
LogPSGCommandlet: ===================================================
LogPSGCommandlet: Scan path:       /Game
LogPSGCommandlet: Fail on error:   YES
LogPSGCommandlet: Fail on warning: no
LogPSGCommandlet: Naming rules: 37  |  Folder rules: 1
LogPSGCommandlet: Scanning assets...
LogPSGCommandlet: Scanned 25 asset(s).
LogPSGCommandlet: ---------------------------------------------------
LogPSGCommandlet: Results: 8 issue(s)  |  7 error(s)  |  1 warning(s)
LogPSGCommandlet: ---------------------------------------------------
LogPSGCommandlet:   [ERROR] [Naming] /Game/Materials/Ground_Dirty - Missing prefix 'M_'.
LogPSGCommandlet:   [WARN ] [Folder] /Game/WrongFolder/M_Used - Expected under: /Game/Materials
LogPSGCommandlet: JSON report: G:\Reports\psg_report.json
LogPSGCommandlet: ===================================================
LogPSGCommandlet: FAILED: 7 error(s) found. (-failonerror)
```

With `-quiet`, individual `[ERROR]`/`[WARN]` lines are suppressed — only the summary and report paths are shown.

---

## JSON Report Format

```json
{
  "tool": "ProjectStructureGuard",
  "version": "1.0.0",
  "timestamp": "2026-04-11T18:23:52",
  "assets_scanned": 25,
  "total_issues": 8,
  "errors": 7,
  "warnings": 1,
  "issues": [
    {
      "asset": "/Game/Materials/Ground_Dirty",
      "severity": "error",
      "type": "naming",
      "description": "Ground_Dirty - Missing prefix 'M_'. Asset name: 'Ground_Dirty'.",
      "suggested_name": "M_Ground_Dirty",
      "suggested_folder": "",
      "auto_fixable": true
    }
  ]
}
```

---

## CSV Report Format

```csv
# PSG Report - 2026.04.11-18.23.52
# Assets scanned: 25  |  Issues found: 8
# Errors: 7  |  Warnings: 1  |  Auto-fixable: 6

Severity,Asset,PackagePath,Type,Description,SuggestedFix,AutoFixable
Error,Ground_Dirty,/Game/Materials/Ground_Dirty,Naming,...,M_Ground_Dirty,Yes
Warning,M_Used,/Game/WrongFolder/M_Used,Folder,...,/Game/Materials,Yes
```

---

## CI/CD Examples

### GitHub Actions

```yaml
- name: Validate Asset Structure
  run: |
    "${{ env.UE_CMD }}" "${{ env.UPROJECT }}" \
      -run=PSGValidate \
      -failonerror \
      -outputjson="${{ github.workspace }}/psg_report.json" \
      -stdout -unattended
```

### Jenkins Pipeline

```groovy
stage('Asset Validation') {
    steps {
        bat '"C:\\UE_5.7\\Engine\\Binaries\\Win64\\UnrealEditor-Cmd.exe" "%UPROJECT%" -run=PSGValidate -failonerror -outputjson="%WORKSPACE%\\psg_report.json" -stdout -unattended'
    }
}
```

### Pre-Commit Hook (Batch)

```batch
@echo off
"E:\UE_5.7\Engine\Binaries\Win64\UnrealEditor-Cmd.exe" "G:\MyProject\MyProject.uproject" -run=PSGValidate -failonerror -quiet -stdout -unattended
if %ERRORLEVEL% NEQ 0 (
    echo PSG: Asset violations detected. Commit blocked.
    exit /b 1
)
```
