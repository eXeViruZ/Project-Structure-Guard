# 02 — Getting Started

## UI Overview

The Project Structure Guard window has three main tabs:

| Tab | Purpose |
|-----|---------|
| **Validation** | Run scans, view results, apply fixes |
| **Unused Assets** | Find and remove unreferenced assets |
| **Rules** | Enable/disable individual rules per project |

---

## Toolbar — Scan Buttons

| Button | Scope |
|--------|-------|
| Scan Whole Project | Scans everything under `/Game` |
| Scan Selected Folder | Scans the folder selected in the Content Browser |
| Scan Selected Assets | Scans only the assets selected in the Content Browser |

---

## Your First Scan

1. Open the PSG window via **Tools → Project Structure Guard**.
2. Click **Scan Whole Project**.
3. Wait for the scan to complete. The status bar shows progress.
4. Results appear in the list below the toolbar.
5. Each row shows: Severity, Asset name, Package path, Issue type, Description, Suggested fix, and whether it is auto-fixable.

---

## Reading Results

- **Error** rows (red) — violations that must be fixed for a clean project.
- **Warning** rows (yellow) — violations that are recommended to fix.
- **Auto-fixable** — PSG can rename or move this asset automatically.

---

## Summary Bar

The bottom bar shows:

```
Errors: X   Warnings: X   Rename-fixable: X   Move-fixable: X   Showing: X
```
