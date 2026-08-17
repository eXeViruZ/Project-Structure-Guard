# 09 — Changelog

All notable changes to Project Structure Guard are documented here.

> **Engine compatibility:** v1.2.0 targets Unreal Engine 5.8. Unreal Engine 5.7 remains supported through the earlier v1.1.1 release.

---

## [1.2.0] — 2026-08-17

### Added

- **Baseline Tracking**
  - Classifies findings as New, Existing, Resolved, or Unclassified.
  - Baselines can be created, updated, cleared, and inspected from Project Structure Guard.
  - Configurable project-relative baseline path supports source-control workflows.

- **Protected Paths**
  - Protected content remains visible in validation.
  - Rename, move, and applicable auto-fix operations are blocked with clear reasons.

- **Validation Results Search**
  - Case-insensitive search across asset/path, issue information, suggested fixes, severity, baseline state, and related result fields.
  - Search combines with existing filters and narrows bulk-action candidates.

- **Rule Ordering, Rule Search/Filters, and Test Rule**
  - Reorder rules by priority with persistence across editor restarts.
  - Search/filter larger rule configurations.
  - Test individual rules in read-only mode.

- **Content Browser Integration**
  - Run scoped validation for selected assets/folders.
  - Open relevant fix/move workflows from selected Content Browser content.

- **Restore from Quarantine**
  - Restore managed quarantined assets to their recorded original locations with safety checks.

- **Baseline-aware CI policy**
  - Added `-failonnew` to fail automated validation when newly introduced findings are detected relative to the configured baseline.

### Improved

- **Bulk Preview 2.0**
  - Expanded rename/move preflight with Ready, Blocked, Skipped, and Conflict states.
  - Added clearer detailed reasons for blocked or conflicting operations.
  - Existing destination and destination-conflict handling is fail-safe.

- **Result Details**
  - Refreshed inspector with asset, class, package path, issue type, severity, issue state, description, suggested fix, expected/actual values, auto-fixability, protection status, and block reason.
  - Added collapsed Advanced Details for rule and issue identity information.

- **Unused Asset and Quarantine Workflows**
  - Improved handling of generated Blueprint artifacts, redirectors, and managed quarantine content.
  - Permanent Delete is guarded and restricted to managed quarantined assets that satisfy the safety checks.
  - External referencers block destructive deletion.

- **CSV and JSON Reports**
  - Expanded report context with baseline state, rule/issue identity, expected/actual values, protection information, and block reasons.

- **Operation Safety and Path Handling**
  - Strengthened boundary-safe path matching and structural-operation preflight behavior.

---

## [1.1.1] — 2026

### Improved / Fixed

- Fixed selected-folder scanning behavior.
- Normalized configured folder paths, including trimming and leading/trailing path handling.
- Improved blocked reasons for rename and move workflows.
- Added CSV output support to the commandlet reporting workflow.
- Improved Move Selected / Move All Safe destination-path handling.
- General UI and workflow refinements.

---

## [1.1.0] — 2026-04-22

### Added

- **Rules Tab** — dedicated tab in the PSG window.
  - Inline checkbox to enable or disable each rule individually without opening Project Settings.
  - Severity and description columns for quick rule overview.
  - Changes persist through project configuration.
  - Rule list refreshes after preset load or JSON import.

- **Validation Result Type Filter**
  - Naming and Folder result-type toggles.
  - Combines with the existing Severity and Auto-fixable filters.

- **Bulk Fix Preview Dialog**
  - Preview before Fix All Safe and Move All Safe.
  - Planned actions can be reviewed before execution.
  - Select All / Select None and per-item selection controls.
  - Cancel closes the preview without applying changes.

### Changed

- Plugin version updated to v1.1.0.
- Product description and source metadata updated for the release.

---

## [1.0.0] — 2026-04-01

### Added

- Naming and folder rule validation.
- Auto-Fix Rename — Fix Selected and Fix All Safe.
- Auto-Fix Move — Move Selected and Move All Safe.
- Redirector cleanup workflow after rename/move operations.
- On-Save Validation with editor notifications.
- Built-in Epic Official, Allar Style Guide, and Lyra presets.
- JSON rule import/export.
- Unused Asset Scanner with quarantine workflow.
- CI/CD commandlet with JSON/CSV reporting and configurable failure policies.
- Validation result filtering and sorting.
- Content Browser navigation from validation results.
- Validation summary counts.
