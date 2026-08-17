# 04 — Auto-Fix & Bulk Preview

> This page describes **Project Structure Guard v1.2.0 for Unreal Engine 5.8**.

## Overview

Project Structure Guard can prepare supported rename and move operations for validation findings and show the planned changes before execution.

The v1.2 workflow emphasizes preflight validation so blocked or conflicting operations are identified before project content is modified.

---

## Rename and Move Workflows

Supported actions include selected-item and bulk workflows for fixable naming and folder violations.

Use the preview whenever multiple structural changes are planned. The preview lets you review which operations are safe to execute and which ones require attention first.

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
3. Select the supported rename or move workflow.
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
