# 02 - Getting Started

> **v1.3.0 documentation preview**, UE 5.8. Until the new version is publicly available, v1.2.0 remains the active Fab release.

## The Six Main Tabs

| Tab | Purpose |
|---|---|
| **Validation** | Scan project content, filter results, inspect findings, review baselines and preview safe fixes |
| **Unused Assets** | Find possible unused assets, manage Quarantine and Restore, and review guarded deletion |
| **Rules** | Search/reorder/toggle global rules, test a rule and preview global toggle impact |
| **Inspector** | Explain effective scoped policies and rules for one asset or folder |
| **Policy Diagnostics** | Read-only configuration warnings and informational notes |
| **Adopt Project** | Guided whole-project review and optional initial baseline setup |

The window uses local, per-user/per-project sizing for supported Validation, Rules and Unused Assets tables and panels. Use each view's reset control to restore its default widths.

## First Scan

1. Open **Tools > Project Structure Guard** and choose **Validation**.
2. Select **Scan Whole Project** for a broad starting point. Selected-folder and selected-asset scans are also available.
3. Check scanned asset count, finding count, errors/warnings and baseline state.
4. Combine **Severity**, **Type**, **State** and **Options** filters with results Search.
5. Select a finding and review its main details and optional Advanced Details.
6. For a supported rename/move workflow, inspect the preview's Ready/Blocked/Skipped/Conflict statuses before applying anything.

## Configure Rules

The global defaults are starter naming conventions, not a substitute for project review. Configure rules under **Project Settings > Project Structure Guard**, or use **Rules** and the built-in presets.

For different content areas, add **Scoped Policies** for `/Game/...` folder paths. More specific scopes can replace individual policy categories while inheriting others. Read the [Scoped Policies guide](10_Policies_Inspector_Diagnostics.md) before relying on intentional empty overrides.

To understand why an asset receives a particular rule, use **Inspector**. To check the rule setup itself, use **Policy Diagnostics**. Both are read-only.

## Baselines for Existing Projects

An accepted baseline helps distinguish **New** from **Existing** findings. It is not a remediation record.

- **Create Baseline** requires a missing file.
- **Update Baseline** is a separate explicit operation that can accept new findings.
- **Review Baseline** explains stored/matched/unmatched entries and uncertainty.
- **Remove Selected Baseline Entries** operates only on selected unmatched entries after a safe whole-project review and confirmation. It does **not** fix assets.
- **Adopt Project** guides an initial scan, findings review, baseline status review and eligible creation/retention actions.

See [Baseline Review and Adoption](11_Baselines_Adoption.md).

## CI and Reporting

Use `PSGValidate` for headless scans and CSV/JSON exports. v1.3 introduces explicit **Development**, **PullRequest** and **Release** gates; existing legacy `-failonerror/-failonwarning/-failonnew` jobs remain supported. See [CI/CD Commandlet](07_Commandlet.md).

## Next Steps

- [Validation details](03_Validation.md)
- [Rule Manager and Impact Preview](05_Rule_Manager.md)
- [Auto-Fix and Bulk Preview](04_Auto_Fix.md)
- [Unused Assets](06_Unused_Assets.md)
- [Policies, Inspector and Diagnostics](10_Policies_Inspector_Diagnostics.md)
- [Baselines and Adoption](11_Baselines_Adoption.md)
