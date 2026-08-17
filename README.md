# Project Structure Guard

**Project structure validation, safe fixing, baseline tracking, and cleanup workflows for Unreal Engine.**

Project Structure Guard helps enforce naming and folder conventions across Unreal Engine projects before structural problems become long-term technical debt. It combines validation, searchable results, safe rename/move previews, baseline-aware issue tracking, protected paths, unused-asset cleanup, reporting, and CI/CD validation in one editor-only C++ plugin.

> **Current documentation target:** Project Structure Guard v1.2.0 for Unreal Engine 5.8.
>
> Unreal Engine 5.7 remains supported through the earlier v1.1.1 release. v1.2.0 itself targets Unreal Engine 5.8 only.

## Product Showcase

[Watch the Project Structure Guard v1.2 showcase on YouTube](https://youtu.be/wDlVkgT0nPU)

---

## Key Features

- **Naming & Folder Validation** — Validate whole-project, selected-folder, and selected-asset scopes.
- **Validation Results Search** — Search large result sets by asset, path, issue information, suggested fixes, severity, and baseline state.
- **Result Details Inspector** — Inspect asset, class, package path, issue type, severity, issue state, suggested fix, expected/actual values, protection state, block reason, and advanced rule/issue identity details.
- **Safe Rename & Move Workflows** — Preview structural changes before execution with preflight checks and detailed Ready, Blocked, Skipped, and Conflict states.
- **Baseline Tracking** — Classify findings as New, Existing, Resolved, or Unclassified against an accepted project baseline.
- **Protected Paths** — Keep violations visible while blocking rename, move, and applicable auto-fix operations inside protected content.
- **Rule Management** — Enable/disable, reorder, search/filter, and test rules in read-only mode.
- **Built-in Presets** — Epic Official, Allar Style Guide, and Lyra presets.
- **Content Browser Integration** — Run scoped validation and open relevant fix/move workflows directly from selected content.
- **On-Save Validation** — Surface structural violations during normal editor work.
- **Unused Asset Cleanup** — Review unused content, move it to managed Quarantine, restore it to recorded original locations, and use guarded Permanent Delete for managed quarantined assets.
- **CSV & JSON Reports** — Export detailed validation data for review, source-controlled workflows, and automation.
- **CI/CD Commandlet** — Run validation headlessly with `-failonerror`, `-failonwarning`, and baseline-aware `-failonnew` policies.
- **Rule Sharing** — Export and import project rule configurations as JSON.

---

## Quick Start

1. Install the plugin for the Unreal Engine version you use.
2. Enable **Project Structure Guard** in **Edit → Plugins** and restart the editor if prompted.
3. Open **Tools → Project Structure Guard**.
4. Configure your own rules or load one of the built-in presets.
5. Run **Scan Whole Project**, **Scan Selected Folder**, or **Scan Selected Assets**.
6. Search/filter the findings, inspect Result Details, and preview supported fixes before applying changes.
7. For ongoing projects, create a baseline once the current accepted state is ready to track future New findings separately.

For the full workflow, start with [Getting Started](docs/02_Getting_Started.md).

---

## Documentation

| Page | Description |
|---|---|
| [Documentation Index](docs/INDEX.md) | Documentation overview and version compatibility |
| [Installation](docs/01_Installation.md) | Requirements, installation, enabling, and updating |
| [Getting Started](docs/02_Getting_Started.md) | UI overview, first scan, search, details, and baseline basics |
| [Validation](docs/03_Validation.md) | Validation scopes, filters, search, Result Details, Baseline Tracking, Protected Paths, and On-Save workflows |
| [Auto-Fix & Bulk Preview](docs/04_Auto_Fix.md) | Rename/move workflows, Bulk Preview 2.0, preflight states, and safety behavior |
| [Rule Manager](docs/05_Rule_Manager.md) | Rule ordering, search/filter, Test Rule, presets, and JSON sharing |
| [Unused Assets](docs/06_Unused_Assets.md) | Scanner, Quarantine, Restore, Permanent Delete safeguards, and limitations |
| [CI/CD Commandlet](docs/07_Commandlet.md) | Headless validation, reports, exit policies, and `-failonnew` |
| [Troubleshooting](docs/08_Troubleshooting.md) | Common issues, blocked operations, baseline, quarantine, and commandlet troubleshooting |
| [Changelog](docs/09_Changelog.md) | Version history |

---

## Engine Compatibility

| Plugin Version | Unreal Engine | Status |
|---|---|---|
| v1.2.0 | UE 5.8 | Current documentation target |
| v1.1.1 | UE 5.7 | Supported UE 5.7 release |

The v1.2 documentation describes the UE 5.8 release. Some workflows and UI elements documented here are not present in v1.1.1.

---

## Support

- **Discord:** [Hanke Unreal Tools](https://discord.gg/vgpmnN6nCR)
- **GitHub Issues:** [eXeViruZ/Project-Structure-Guard](https://github.com/eXeViruZ/Project-Structure-Guard/issues)
- **Showcase:** [Project Structure Guard v1.2](https://youtu.be/wDlVkgT0nPU)

© 2026 Tom Leon Vincent Hanke
