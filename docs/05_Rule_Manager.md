# 05 — Rule Manager

> This page describes **Project Structure Guard v1.3.0 release preparation for Unreal Engine 5.8 (not yet publicly available on Fab)**.

## Overview

The **Rules** area gives direct control over the naming and folder rules used by validation.

Project Structure Guard v1.2 adds rule ordering, rule search/filtering, and a read-only Test Rule workflow on top of the existing enable/disable, preset, import, and export functionality.

---

## Rule Types

Project Structure Guard manages two primary rule groups:

- **Naming Rules** — define expected naming conventions for applicable asset classes.
- **Folder Rules** — define required project locations for applicable asset classes.

---

## Enable and Disable Rules

Individual rules can be enabled or disabled directly from the Rule Manager.

Changes affect subsequent validation scans and are persisted in the project configuration.

Use per-rule toggles when a project intentionally does not use a specific convention from a larger preset or shared ruleset.

---

## Rule Ordering

Rules can be reordered by priority.

The configured order persists across editor restarts.

Keep more specific project rules intentionally ordered so the active configuration remains understandable to other team members and future maintainers.

---

## Rule Search and Filters

Use the Rule Manager search/filter controls to narrow larger rule configurations.

This is especially useful when working with preset-derived configurations or project-specific rule sets containing many asset classes.

Search/filtering changes what is shown in the Rule Manager; it does not silently delete or disable hidden rules.

---

## Test Rule

The **Test Rule** workflow allows a configured rule to be checked in read-only mode.

Use it to inspect how a rule behaves before relying on it in normal validation or structural fix workflows.

Testing a rule does not perform rename/move operations on project content.

---

## Built-in Presets

Project Structure Guard includes three ready-to-use rule presets:

| Preset | Basis |
|---|---|
| **Epic Official** | Unreal Engine naming conventions |
| **Allar Style Guide** | Gamemakin UE Style Guide by Allar |
| **Lyra** | Naming conventions based on Epic's Lyra sample project |

Loading a preset replaces the active rule configuration with the selected preset data. Export important custom rules before replacing them.

---

## JSON Rule Export

Use **Export Rules** to save the current naming and folder rule configuration as JSON.

The exported file is suitable for:

- Source control
- Team sharing
- Backing up project-specific rules
- Moving rule configurations between compatible projects

---

## JSON Rule Import

Use **Import Rules** to load a previously exported Project Structure Guard ruleset.

Review imported rules after loading, especially when moving configuration between projects with different folder structures or naming requirements.

---

## Source-Control Workflow

For teams, keep shared Project Structure Guard configuration in source control alongside the project where practical.

A recommended workflow is:

1. Agree on naming/folder standards.
2. Configure or import the ruleset.
3. Review rule ordering and enabled states.
4. Use Test Rule for focused checks where needed.
5. Commit the project configuration.
6. Review rule changes like any other project configuration change.

Baseline data can also be stored in a project-relative location for source-control workflows.

---

## v1.3: Scoped Policies

Global naming/folder rules remain the fallback. **Project Settings > Project Structure Guard** also supports independent per-folder **Scoped Policies** for Naming Rules, Folder Rules, Excluded Paths and Protected Paths. A more specific matching scope can override one category while inheriting other categories. An explicitly enabled empty override intentionally clears the inherited category. See [Scoped Policies, Inspector and Diagnostics](10_Policies_Inspector_Diagnostics.md).

The Rules tab primarily presents **global** naming/folder rule ordering, enabling and testing. Do not confuse the global list with the full effective policy inside a scoped folder. Use **Inspector** to see the effective result for a selected path.

## v1.3: Preview Toggle Impact

Select exactly one existing global Naming Rule or Folder Rule and choose **Preview Toggle Impact**. The read-only preview uses the existing project scan/validation logic to compare findings before and after a hypothetical Enabled toggle. It reports Added, No longer reported, Unchanged, affected assets, and applicable first-match rule changes.

The preview does not alter the rule, assets, baseline or settings. It does not support modifying rule signatures, drafting new rules or previewing scoped overrides. “No longer reported” is not evidence that an underlying asset was fixed.

## Replacing Rulesets Safely

In v1.3, choosing a built-in preset or JSON rule import presents an explicit replacement confirmation. **Cancel** does not apply the replacement. A confirmed replacement can change rule order, identities and the baseline classification of findings; keep a backup/export of important project rules and review any baseline impact before accepting changes.

The Rules view supports locally persistent Naming/Folder table column widths and split ratios, with **Reset Rules Layout** to restore defaults. Layout storage is per user/project and separate from shared rule settings.
