# 07 - CI/CD Commandlet

> Documentation for the upcoming **Project Structure Guard v1.3.0** on Unreal Engine 5.8. The public Fab version remains v1.2.0 until the update is approved and available.

## Overview

`PSGValidate` uses the existing project naming/folder rule configuration, scoped policies, scan, validation and baseline systems. It writes machine-readable CSV/JSON reports and returns exit codes suitable for CI. It does not apply fixes.

## Basic Command

On Windows, using the UE 5.8 editor commandlet executable:

```powershell
& "E:\UE_5.8\Engine\Binaries\Win64\UnrealEditor-Cmd.exe" "C:\Projects\MyGame\MyGame.uproject" -run=PSGValidate -unattended -nop4 -nosplash
```

Adapt executable and project paths to your installation. Run it against the desired project configuration; the plugin must be installed and enabled for that project.

## v1.3 CI Gate Profiles

Select a profile **explicitly** with `-profile=...`:

| Value | Gate contract |
|---|---|
| `Development` | Generate validation results without failing solely because findings exist. |
| `PullRequest` | Fail on **New** findings (exit 1). Requires a readable, valid baseline; otherwise exit 2. |
| `Release` | Fail on current **Error** findings (exit 1); warnings alone do not fail this gate. A baseline is optional. |
| `ProjectDefault` | Explicitly use the `DefaultCIGateProfile` configured in Project Settings (code default: `PullRequest`). This selects a profile; it is not a separate gate policy. |

**No implicit profile:** Without `-profile`, PSG preserves the existing legacy commandlet flag behavior. Selecting a project default in settings does not silently change old automation jobs.

## Usage Examples

```powershell
# Development reporting
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate -profile=Development -unattended -nop4

# PR gate with a committed, valid baseline
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate -profile=PullRequest -outputcsv="Saved/PSGReports/pr.csv" -unattended -nop4

# Release error gate
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate -profile=Release -outputjson="Saved/PSGReports/release.json" -unattended -nop4

# Explicit project-configured profile
UnrealEditor-Cmd.exe "MyGame.uproject" -run=PSGValidate -profile=ProjectDefault -unattended -nop4
```

## Legacy Options

| Flag | Meaning |
|---|---|
| `-failonerror` | Legacy failure policy for Error findings |
| `-failonwarning` | Legacy failure policy for Warning findings |
| `-failonnew` | Legacy baseline-aware failure policy for New findings |
| `-scanpath=/Game/Folder` | Limit scanning to a particular internal package folder |
| `-outputcsv=<path>` | Explicit CSV report path |
| `-outputjson=<path>` | Explicit JSON report path |
| `-quiet` | Reduce per-finding log detail |

Do **not** combine `-profile` with `-failonerror`, `-failonwarning` or `-failonnew`. Invalid, duplicated or conflicting profile arguments fail with exit **2**.

A `-scanpath` restriction produces a scoped scan. It does not by itself prove whole-project compliance. Use a full scan where the CI policy is intended to cover the full project.

## Process Exit Codes

| Exit | Interpretation |
|---|---|
| `0` | Validation completed and the active gate passed |
| `1` | Validation completed but a configured finding gate rejected the results |
| `2` | Invalid/conflicting arguments or another required CI prerequisite/reporting operation failed in profile mode |

**Exit 1 is not necessarily a plugin crash.** A correctly functioning PullRequest gate can reject new findings. For PullRequest, an invalid/missing required baseline is a configuration/prerequisite error, not an automatic acceptance of findings.

Profile-mode explicit report-output failures are treated as errors. In legacy mode, existing output/recovery behaviors are preserved for compatibility.

## Baseline and Source Control

Keep your baseline JSON and shared policy settings in source control where appropriate. Review updates explicitly. A changed issue identity after a rename, move or rule edit may be classified differently, even when the underlying project issue remains.

See [Baseline Review and Adoption](11_Baselines_Adoption.md) and [Scoped Policies](10_Policies_Inspector_Diagnostics.md).

## Safety Notes

The commandlet reports findings and does not modify assets as part of ordinary validation. Run automation with the same UE 5.8 version and the same rules/baseline paths across team machines. Archive the CSV/JSON results and the commandlet log for debugging.
