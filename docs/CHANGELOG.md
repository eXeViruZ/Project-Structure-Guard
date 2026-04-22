# Changelog — Project Structure Guard

## [1.1.0] — 2026-04-22

### Added
- **Rules Tab** — Per-rule enable/disable toggle with inline checkbox, persisted via SaveConfig(). Refreshes after preset load or JSON import.
- **Validation Result Type Filter** — Naming / Folder toggle buttons in the filter toolbar, combinable with existing Severity filters.
- **Fix Preview Dialog** — Modal dry-run confirmation before Fix All Safe and Move All Safe. Per-row checkbox to skip individual actions. Select All / Select None toolbar. Live action count footer.

### Changed
- `Version` bumped to `2`, `VersionName` to `1.1.0`.
- Plugin description updated.

---

## [1.0.0] — 2026-04-01

### Added
- Validation engine (naming + folder rules).
- Auto-Fix Rename (`FPSGRenameService`) — Fix Selected / Fix All Safe.
- Auto-Fix Move (`FPSGMoveService`) — Move Selected / Move All Safe.
- Redirector Cleanup after rename/move.
- Preset Rule Sets (Epic Official, Allar, Lyra).
- JSON Rule Import/Export (`FPSGRuleSetService`).
- Unused Asset Scanner tab.
- CI/CD Commandlet (`-run=PSGValidate`) with `-outputjson`, `-outputcsv`, `-failonerror`, `-failonwarning`, `-scanpath`, `-quiet`.
- CSV Export to `Saved/PSGReports/`.
- Result filtering (Errors / Warnings / Auto-fixable only).
- Column sorting, double-click to navigate, summary bar.
