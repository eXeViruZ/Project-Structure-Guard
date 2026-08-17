# 05 — Rule Manager

> This page describes **Project Structure Guard v1.2.0 for Unreal Engine 5.8**.

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
