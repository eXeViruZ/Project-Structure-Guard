# 02 — Getting Started

> This page describes **Project Structure Guard v1.2.0 for Unreal Engine 5.8**. Unreal Engine 5.7 remains supported through v1.1.1, but some v1.2 workflows described here are not available there.

## UI Overview

Project Structure Guard is organized around three main workflow areas:

| Area | Purpose |
|---|---|
| **Validation** | Scan project content, search/filter findings, inspect Result Details, and preview/apply supported fixes |
| **Unused Assets** | Find unused content and manage Quarantine, Restore, and guarded Permanent Delete workflows |
| **Rules** | Enable/disable, reorder, search/filter, test, import, and export project rules |

---

## Scan Scope

Use the validation controls to scan the scope you need:

| Action | Scope |
|---|---|
| **Scan Whole Project** | Scans project content under `/Game` |
| **Scan Selected Folder** | Scans the selected Content Browser folder |
| **Scan Selected Assets** | Scans only selected Content Browser assets |

Scoped validation can also be started from supported Content Browser actions.

---

## Your First Scan

1. Open **Tools → Project Structure Guard**.
2. Click **Scan Whole Project**.
3. Wait for the scan to complete.
4. Review the findings in the Validation Results list.
5. Use Search and the existing filters to narrow the result set.
6. Select a finding to inspect its Result Details.
7. Preview supported rename or move operations before execution.

---

## Search and Filters

Validation Results Search is case-insensitive and works together with the existing filters.

Search can match information including:

- Asset name and asset path
- Current path
- Description
- Expected and actual values
- Suggested name or folder
- Block reason
- Asset class
- Rule display name
- Issue type, severity, and baseline state labels

Filters and Search are combined, so you can progressively narrow larger result sets.

---

## Result Details

Selecting a single finding opens the Result Details inspector.

The main details include:

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

**Advanced Details** keeps lower-level rule and issue identity information available without cluttering the main inspector.

---

## Baseline Basics

A baseline captures an accepted validation state so future scans can distinguish newly introduced issues from already known findings.

Findings can be classified as:

- **New** — introduced after the accepted baseline
- **Existing** — already present in the baseline
- **Resolved** — baseline findings that no longer exist
- **Unclassified** — no applicable baseline classification

A practical workflow is:

1. Bring the project to an accepted state.
2. Create or update the baseline.
3. Continue normal development.
4. Filter future scans by **New** to focus on newly introduced structural violations.

---

## Protected Paths

Protected Paths allow important folders to remain visible in validation while blocking rename, move, and applicable auto-fix operations that would modify protected content.

When an operation is blocked, Project Structure Guard keeps the finding visible and exposes the reason in the result/preflight information.

---

## Next Steps

- [Validation](03_Validation.md) — rules, search, filters, baselines, protected paths, On-Save Validation
- [Auto-Fix & Bulk Preview](04_Auto_Fix.md) — rename/move previews and safety states
- [Rule Manager](05_Rule_Manager.md) — ordering, search/filter, Test Rule, presets, JSON sharing
- [Unused Assets](06_Unused_Assets.md) — Quarantine, Restore, and guarded deletion
- [CI/CD Commandlet](07_Commandlet.md) — automated validation and `-failonnew`
