# 03 — Validation

> This page describes **Project Structure Guard v1.2.0 for Unreal Engine 5.8**.

## How Validation Works

Project Structure Guard validates scanned assets against configured naming and folder rules.

- **Naming Rules** — validate expected prefixes, suffixes, and applicable asset classes.
- **Folder Rules** — validate that assets are stored under the required project paths.

Violations are collected in the Validation Results view, where they can be searched, filtered, inspected, and used as input for supported fix workflows.

---

## Validation Scopes

Validation can run against:

- The whole project
- A selected Content Browser folder
- Selected Content Browser assets

Supported Content Browser actions also provide scoped entry points into validation and fix/move workflows.

---

## Result Filters

The Validation Results toolbar can narrow the current result set by available issue properties such as severity, issue type, baseline state, and auto-fixability.

Filters are combinable and also work together with Validation Results Search.

---

## Validation Results Search

Search is case-insensitive and uses trimmed substring matching.

Searchable information includes:

- Asset path and asset name
- Current path
- Description
- Expected value
- Actual value
- Suggested name
- Suggested folder
- Block reason
- Asset class
- Rule display name
- Issue type labels
- Severity labels
- Baseline state labels

Search does not expose low-level identity fields such as Issue ID, Rule ID, or Rule Signature Hash as normal searchable content.

Because Search is part of the active result filtering pipeline, supported bulk actions operate on the currently filtered result set.

---

## Result Details

Select a single validation finding to inspect detailed information without leaving the Validation view.

### Main Details

- Asset
- Asset Class
- Package Path
- Issue Type
- Severity
- Issue State
- Description
- Suggested Fix
- Expected Value
- Actual Value
- Auto-Fixable
- Protected
- Block Reason

Empty values are shown as an em dash.

### Advanced Details

The collapsed **Advanced Details** section exposes lower-level identity information when needed:

- Rule Display Name
- Rule ID
- Issue ID
- Rule Signature Hash

If a selected row is filtered out, the selection is cleared so the inspector cannot display stale hidden data.

---

## Baseline Tracking

Baseline Tracking lets you capture an accepted validation state and compare future scans against it.

Findings can be classified as:

| State | Meaning |
|---|---|
| **New** | The finding was introduced after the baseline |
| **Existing** | The finding already exists in the accepted baseline |
| **Resolved** | A baseline finding is no longer present |
| **Unclassified** | No applicable baseline state could be assigned |

Project Structure Guard provides controls to create, update, clear, and inspect baseline status.

The baseline path is configurable and project-relative, allowing baseline files to participate in source-control workflows.

A common workflow is to accept the current project state as the baseline and then use the **New** state to focus future reviews and CI checks on newly introduced problems.

---

## Protected Paths

Protected Paths prevent supported structural modification workflows from changing critical project content while still keeping violations visible.

When content falls under a protected path:

- The validation finding remains visible.
- Rename, move, and applicable auto-fix operations are blocked.
- The UI exposes a clear block reason.

This allows teams to enforce conventions without hiding problems or allowing critical folders to be changed unintentionally.

---

## Navigate to Assets

Double-click supported result rows to locate the affected asset in the Content Browser.

---

## On-Save Validation

On-Save Validation can surface structural issues while assets are being saved.

Configure the feature in **Project Settings → Project Structure Guard**.

This keeps validation integrated into the normal editor workflow instead of relying only on later cleanup passes.

---

## Related Documentation

- [Auto-Fix & Bulk Preview](04_Auto_Fix.md)
- [Rule Manager](05_Rule_Manager.md)
- [CI/CD Commandlet](07_Commandlet.md)
