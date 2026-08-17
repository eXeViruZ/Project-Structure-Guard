# 07 — CI/CD Commandlet

> This page describes **Project Structure Guard v1.2.0 for Unreal Engine 5.8**.

## Overview

Project Structure Guard includes a headless validation commandlet for CI/CD and automated project checks.

The commandlet can:

- Scan project content without opening the normal editor UI
- Export CSV and JSON reports
- Fail on Error-severity findings
- Fail on Warning findings
- Fail only when findings are **New** relative to the configured baseline

---

## Basic Usage

```bash
UnrealEditor-Cmd.exe "[YourProject].uproject" -run=PSGValidate
```

Use the command-line executable appropriate for your Unreal Engine installation and platform.

---

## Main Options

| Flag | Description |
|---|---|
| `-outputjson=<path>` | Write a JSON validation report to the specified path |
| `-outputcsv=<path>` | Write a CSV validation report to the specified path |
| `-failonerror` | Return a failing exit code when Error-severity findings are present |
| `-failonwarning` | Return a failing exit code when Warning/Error findings trigger the policy |
| `-failonnew` | Return a failing exit code when New baseline-aware findings are present |
| `-scanpath=<path>` | Limit the scan to a package path such as `/Game/Characters` |
| `-quiet` | Reduce per-finding commandlet log output |

---

## Baseline-Aware `-failonnew`

`-failonnew` is intended for teams that want CI to block newly introduced structural problems without failing continuously because of already accepted legacy findings.

Typical workflow:

1. Create or update the accepted Project Structure Guard baseline in the editor.
2. Keep the project-relative baseline file in source control where appropriate.
3. Run the commandlet with `-failonnew` in CI.
4. Existing accepted findings remain distinguishable from newly introduced findings.
5. CI fails when New findings trigger the policy.

If no applicable baseline classification is available, review the commandlet output and baseline configuration before relying on `-failonnew` as a gate.

---

## Examples

### Fail on errors

```bash
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate -failonerror
```

### Export JSON and CSV

```bash
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate \
  -outputjson="Saved/PSGReports/psg.json" \
  -outputcsv="Saved/PSGReports/psg.csv"
```

### Baseline-aware CI validation

```bash
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate \
  -outputjson="Saved/PSGReports/psg.json" \
  -outputcsv="Saved/PSGReports/psg.csv" \
  -failonnew \
  -quiet \
  -unattended \
  -nop4
```

### Scan a subfolder

```bash
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate \
  -scanpath=/Game/Characters \
  -failonerror
```

---

## Reports

The v1.2 CSV/JSON reports contain richer validation context than earlier releases, including information such as:

- Severity
- Asset/path data
- Issue type and description
- Suggested fix information
- Auto-fixability
- Baseline/issue state
- Rule and issue identity
- Expected and actual values
- Protection information
- Block reasons

Use the machine-readable report formats for CI artifacts, review, or downstream tooling.

---

## Exit Behavior

A non-zero result can be an expected policy outcome rather than an internal plugin failure.

For example, a run with `-failonnew` should return a failing result when New findings are detected. CI should treat that as a validation gate failure and surface the generated report/log to the team.

Internal commandlet errors should be investigated separately from policy-driven validation failures.

---

## CI Recommendations

- Keep the Unreal Engine version used by CI aligned with the plugin package.
- For v1.2.0, run the commandlet with **UE 5.8**.
- Store baseline/rule configuration in source control when using shared team policies.
- Archive the JSON/CSV report when a validation gate fails.
- Prefer `-failonnew` when adopting PSG in an existing project with accepted legacy violations.
- Re-run the same command locally when diagnosing CI-only differences.
