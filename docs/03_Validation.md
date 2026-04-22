# 03 — Validation

## How Validation Works

PSG validates each scanned asset against two rule sets defined in **Project Settings → Project Structure Guard**:

- **Naming Rules** — check asset prefix, suffix, and class type
- **Folder Rules** — check that an asset lives in its required folder path

Violations are collected and displayed in the Validation tab.

---

## Configuring Rules

Go to **Edit → Project Settings → Project Structure Guard**.

### Naming Rules

Each naming rule defines:

| Field | Description |
|-------|-------------|
| Asset Class | The Unreal asset class this rule applies to (e.g. `StaticMesh`) |
| Required Prefix | Expected prefix (e.g. `SM_`) |
| Required Suffix | Expected suffix (optional) |
| Severity | Error or Warning |
| Enabled | Whether this rule is active |

### Folder Rules

Each folder rule defines:

| Field | Description |
|-------|-------------|
| Asset Class | The Unreal asset class this rule applies to |
| Required Folder | Package path the asset must live under (e.g. `/Game/Meshes`) |
| Severity | Error or Warning |
| Enabled | Whether this rule is active |

---

## Result Filters

Use the filter toolbar above the result list to narrow down what is shown:

| Filter | Effect |
|--------|--------|
| Errors | Show/hide Error severity rows |
| Warnings | Show/hide Warning severity rows |
| Auto-fixable only | Show only rows that PSG can fix automatically |
| Naming | Show/hide Naming Violation rows |
| Folder | Show/hide Folder Violation rows |

All filters are combinable.

---

## Column Sorting

Click any column header to sort results by that column. Click again to reverse the sort direction.

---

## Navigate to Asset

Double-click any result row to select and highlight the asset in the Content Browser.

---

## On-Save Validation

PSG can validate assets automatically every time you save.

- Enable in **Project Settings → Project Structure Guard → Validate on Save**.
- When a violation is detected on save, a toast notification appears in the editor with the suggested fix.
