# Project Structure Guard

**Project structure validation, scoped policies, baseline tracking and safe cleanup workflows for Unreal Engine.**

Project Structure Guard is an editor-only C++ plugin for enforcing naming and folder conventions without losing visibility into existing project debt. Validate content, preview supported rename/move actions, manage baseline findings, review unused assets and enforce policies in CI.

> **Release status:** v1.3.0 documentation is being prepared for a pending Fab update. **v1.2.0 remains the latest publicly available release** until Fab publishes v1.3.0.
>
> **Engine:** UE 5.8 for v1.2.0 and v1.3.0. The older v1.1.1 package is the UE 5.7 line.

## What is new in v1.3.0?

- **Scoped Project Policies:** Override naming, folder, excluded and protected rules by folder area. Individual categories can inherit or override a parent.
- **Effective Policy Inspector:** Explain which scoped policies and relevant rules apply to one asset or folder, including where they originate.
- **Policy Diagnostics:** Read-only warnings and notes for detectable policy configuration problems.
- **Baseline Review and Manual Reconciliation:** Review mismatched stored entries and selectively remove unmatched entries after explicit confirmation. This does **not** fix assets or accept New findings.
- **Adopt Project:** Guided review of an existing project's rules, findings and baseline status; optionally establish a missing initial baseline without overwriting an existing one.
- **CI Gate Profiles:** Named Development, PullRequest and Release gates plus explicit ProjectDefault resolution in PSGValidate.
- **Policy Impact Preview:** Read-only impact of hypothetically toggling one existing global naming or folder rule.
- **Improved editor workflows:** Clearer six-tab navigation, safer confirmations and locally remembered splitter/table-column sizes.

## Existing Core Features

- Whole-project, selected-folder and selected-asset naming/folder validation.
- Content Browser integration, On-Save Validation, result search, filtering and detailed findings.
- Safe rename/move preflight with Ready, Blocked, Skipped and Conflict states, plus Protected Paths.
- Rule ordering, enable/disable, Test Rule, Epic Official/Allar/Lyra presets and JSON sharing.
- Baseline classification and configurable project-relative baseline files.
- Unused asset review, managed Quarantine, Restore and guarded Permanent Delete.
- CSV/JSON reporting and the PSGValidate commandlet, including legacy -failonerror, -failonwarning and -failonnew flags.

## Quick Start

1. Install the package for your Unreal Engine version and enable **Project Structure Guard** under Edit > Plugins.
2. Open **Tools > Project Structure Guard**.
3. Start in **Validation**, or use **Adopt Project** when bringing PSG into an existing project.
4. Configure global or scoped rules in Project Settings; inspect effective rules in **Inspector**.
5. Run **Scan Whole Project**, review results and use safe previews before any supported structural change.
6. If tracking accepted legacy findings, explicitly create or update a baseline, then review New findings in subsequent scans.
7. For automation, configure and invoke a suitable CI gate profile.

## Documentation

| Page | What it covers |
|---|---|
| [Documentation Index](docs/INDEX.md) | Full documentation, release status and compatibility |
| [Installation](docs/01_Installation.md) | Installation, updating and compatibility |
| [Getting Started](docs/02_Getting_Started.md) | Six-tab tour, first scan and key workflows |
| [Validation](docs/03_Validation.md) | Scopes, finding states, filters and On-Save checks |
| [Auto-Fix & Bulk Preview](docs/04_Auto_Fix.md) | Rename/move safety and redirector cleanup |
| [Rule Manager](docs/05_Rule_Manager.md) | Ordering, imports, Test Rule and toggle preview |
| [Unused Assets](docs/06_Unused_Assets.md) | Unused content, Quarantine and guarded deletion |
| [CI/CD Commandlet](docs/07_Commandlet.md) | Profiles, legacy flags, exit codes and reports |
| [Troubleshooting](docs/08_Troubleshooting.md) | Common problems and safe recovery |
| [Changelog](docs/09_Changelog.md) | Version-specific changes |
| [Scoped Policies and Diagnostics](docs/10_Policies_Inspector_Diagnostics.md) | Scoped inheritance, Inspector, Diagnostics, Impact Preview |
| [Baseline Review and Adoption](docs/11_Baselines_Adoption.md) | Safe initial baseline, review and manual reconciliation |

## Compatibility and Important Limits

| Plugin release | Unreal Engine | Public availability |
|---|---|---|
| **v1.3.0** | **5.8** | Release candidate, pending Fab availability |
| **v1.2.0** | **5.8** | Public release |
| **v1.1.1** | **5.7** | Legacy release |

The plugin descriptor declares Win64, Mac and Linux. v1.3 Win64 BuildPlugin passed; native Mac/Linux compilation and customer-package smoke QA were not confirmed at this documentation checkpoint. **Adopt Project's initial baseline creation requires a supported local Windows filesystem**, and is restricted on Mac/Linux and unsupported sandbox/network filesystem paths. Other read-only features should not be confused with that creation operation.

## Showcase and Support

- **Fab:** https://www.fab.com/listings/7dfc5ec6-1261-4f86-8e69-82ea0ae1e8a2
- **v1.2 video (historical showcase):** https://youtu.be/wDlVkgT0nPU
- **Community and support:** https://discord.gg/vgpmnN6nCR
- **Issues:** https://github.com/eXeViruZ/Project-Structure-Guard/issues
- **Email (alternative):** Tom.Hanke.Official@web.de

© 2026 Tom Leon Vincent Hanke
