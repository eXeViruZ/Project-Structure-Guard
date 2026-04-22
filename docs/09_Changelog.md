# 09 — Changelog

All notable changes to Project Structure Guard are documented here.

---

## [1.1.0] — 2026-04-22

### Added

- **Rules Tab** — New dedicated tab in the PSG window.
  - Inline checkbox to enable or disable each rule individually without opening Project Settings.
  - Severity and description columns for quick rule overview.
  - Changes are persisted immediately via `SaveConfig()`.
  - Rule list refreshes automatically after preset load or JSON import.

- **Validation Result Type Filter** — Two new toggle buttons in the filter toolbar.
  - **Naming** — show or hide Naming Violation rows.
  - **Folder** — show or hide Folder Violation rows.
  - Works in combination with the existing Severity and Auto-fixable filters.

- **Bulk Fix Preview Dialog** — Modal confirmation before Fix All Safe and Move All Safe.
  - Lists every planned action with Apply checkbox, Asset name, and Planned Action.
  - Per-row checkbox to skip individual items before confirming.
  - Select All / Select None toolbar.
  - Live count of selected actions in the footer.
  - Cancel closes the dialog with no changes applied.

### Changed

- `.uplugin` Version bumped to `2`, VersionName to `1.1.0`.
- Plugin description updated to reflect v1.1 features.
- All copyright headers unified across all source files.

---

## [1.0.0] — 2026-04-01

### Added

- Naming rule and folder rule validation engine.
- Auto-Fix Rename (`FPSGRenameService`) — Fix Selected and Fix All Safe.
- Auto-Fix Move (`FPSGMoveService`) — Move Selected and Move All Safe.
- Redirector cleanup after rename and move operations.
- On-Save validation with toast notifications.
- Built-in presets: Epic Official, Allar Style Guide, Lyra Sample Project.
- JSON rule import and export (`FPSGRuleSetService`).
- Unused Asset Scanner with quarantine and delete support.
- CI/CD Commandlet (`-run=PSGValidate`) with `-outputjson`, `-outputcsv`, `-failonerror`, `-failonwarning`, `-scanpath`, `-quiet`.
- CSV export to `Saved/PSGReports/`.
- Result filtering by Errors, Warnings, and Auto-fixable only.
- Column sorting — click any header to sort ascending/descending.
- Double-click any result row to select the asset in the Content Browser.
- Summary bar with live counts of Errors, Warnings, Rename-fixable, Move-fixable, and Showing.
