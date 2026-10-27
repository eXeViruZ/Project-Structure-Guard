# 04 — Auto-Fix & Bulk Preview

> This page describes **Project Structure Guard v1.3.0 release preparation for Unreal Engine 5.8 (not yet publicly available on Fab)**.

## Overview

Project Structure Guard can prepare supported rename and move operations for validation findings and show the planned changes before execution.

The established workflow emphasizes preflight validation so blocked or conflicting operations are identified before project content is modified.

---

## Rename and Move Actions

The Validation UI exposes these actions:

| Group | Action | Purpose |
|---|---|---|
| **Rename** | **Fix Selected** | Prepare naming fixes for the selected applicable findings |
| **Rename** | **Fix All** | Prepare naming fixes for the applicable findings in the active filtered result set |
| **Move** | **Move Selected** | Prepare folder moves for the selected applicable findings |
| **Move** | **Move All** | Prepare folder moves for the applicable findings in the active filtered result set |

`Fix All` and `Move All` do not blindly force every visible finding through. Planned operations are evaluated by the preview/preflight workflow before execution.

---

## Bulk Preview 2.0

Bulk Preview 2.0 performs preflight checks and classifies planned operations before execution.

Typical states include:

| State | Meaning |
|---|---|
| **Ready** | The operation passed preflight and can be executed |
| **Blocked** | The operation is prevented by a safety rule or protected condition |
| **Skipped** | The finding cannot or should not be processed by the current operation |
| **Conflict** | The planned destination conflicts with another asset or planned operation |

The preview exposes detailed reasons so you can understand why a specific item is not Ready.

---

## Preflight Safety Checks

Depending on the operation, Project Structure Guard checks conditions such as:

- Existing destination assets
- Conflicting rename or move targets
- Protected Paths
- Non-fixable findings
- Invalid or blocked destination conditions
- Other operation-specific constraints

If the destination already exists, the operation is blocked instead of silently overwriting project content.

---

## Protected Content

Protected Paths are respected by structural fix workflows.

A protected finding remains visible in Validation Results, but applicable rename, move, and auto-fix operations are blocked and expose a clear reason.

---

## Search and Filter Interaction

Validation Results Search and the existing validation filters narrow the active result set.

Bulk actions use the currently filtered rows, so Search can be used deliberately to limit the candidates shown in a bulk preview.

Always review the resulting preview before execution.

---

## Redirector Cleanup

Rename and move operations can leave Unreal redirectors behind depending on the operation and project state.

Use Project Structure Guard's redirector cleanup workflow when appropriate to run Unreal's redirector fix-up on affected content.

---

## Recommended Workflow

1. Run validation for the required scope.
2. Use Search/filters to isolate the findings you intend to change.
3. Use **Fix Selected / Fix All** for naming violations or **Move Selected / Move All** for folder violations.
4. Review every item in Bulk Preview 2.0.
5. Resolve Blocked or Conflict items instead of forcing them through.
6. Execute only the Ready operations you intend to apply.
7. Re-run validation after structural changes.
8. Save the project and verify important references/content as part of your normal change review.

---

## Safety Notes

- Project Structure Guard does not treat a preflight conflict as a safe operation.
- Protected content is not modified by applicable structural auto-fix workflows.
- A finding being visible does not mean it is safe or eligible for automatic modification.
- Baseline state is classification information; it does not bypass normal preflight or Protected Path checks.

---

## v1.3 Scoped Policy Awareness

Naming/folder rules and excluded or protected paths may differ across project folder scopes. Structural preflight and supported operations evaluate effective project policies rather than assuming that global rule arrays govern every asset. Check the [Effective Policy Inspector](10_Policies_Inspector_Diagnostics.md) to understand why a particular path is excluded or protected.

Before applying a global rule change, **Preview Toggle Impact** in the **Rules** tab can compare findings for a hypothetical enable/disable toggle of one existing global rule. It is read-only, does not preview an asset fix, and does not apply changes. See [Rule Manager](05_Rule_Manager.md).

## v1.3 Review Guidance

Fix Preview clarifies how many selected operations are actually ready. Selecting none disables Apply. A displayed finding, a baseline state or a rule-preview result is **not** proof that an asset is safe to modify. Review each preflight state and back up or commit the project before bulk structural changes.
