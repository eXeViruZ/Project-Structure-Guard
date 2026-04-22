# 04 — Auto-Fix

## Overview

PSG can automatically fix two types of violations:

| Fix Type | What it does |
|----------|--------------|
| **Rename** | Adds the correct prefix/suffix to the asset name |
| **Move** | Moves the asset to its required folder path |

Both operations update all references automatically and create redirectors where needed.

---

## Fix Buttons

| Button | Scope | Preview |
|--------|-------|---------|
| Fix Selected | Rename only the rows selected in the list | No |
| Fix All Safe | Rename all auto-fixable naming violations | Yes — preview dialog |
| Move Selected | Move only the rows selected in the list | No |
| Move All Safe | Move all auto-fixable folder violations | Yes — preview dialog |

---

## Bulk Fix Preview Dialog

When you click **Fix All Safe** or **Move All Safe**, a preview dialog opens before anything is changed.

The dialog shows every planned action:

| Column | Description |
|--------|-------------|
| Apply | Checkbox — uncheck to skip this item |
| Asset | Asset name |
| Planned Action | What will happen (e.g. `Rename → SM_Rock`) |

**Toolbar buttons:**
- **Select All** — check all items
- **Select None** — uncheck all items

**Footer:** shows live count of selected actions.

**Confirm** — applies only the checked items.
**Cancel** — closes the dialog, nothing is changed.

---

## Redirector Cleanup

After rename or move operations, use **Fix Redirectors** to clean up dangling redirectors left behind.

This calls the Unreal Engine built-in redirector fixup on all affected assets.

---

## Safety

- PSG never fixes assets that have ambiguous or conflicting rename targets.
- Assets with no clear single rule match are skipped and reported as blocked.
- Blocked assets are listed in the status bar after a fix operation.
