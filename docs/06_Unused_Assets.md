# 06 — Unused Asset Scanner

## Overview

The **Unused Assets** tab scans your project for assets that are not referenced by any map or other asset.

This helps you identify dead content that is safe to remove, reducing project size and build times.

---

## How It Works

PSG uses the Unreal Asset Registry to trace:
- Direct references
- Indirect references
- Soft references

An asset is considered unused only if it has **no** inbound references of any kind.

---

## Result Columns

| Column | Description |
|--------|-------------|
| Asset Name | Name of the unused asset |
| Asset Class | Unreal class type |
| Package Path | Location in the Content Browser |
| File Size | Disk size of the asset |

Sort by **File Size** to prioritize the largest unused assets first.

---

## Actions

| Button | Effect |
|--------|--------|
| Scan Unused Assets | Run the unused asset scan |
| Delete Selected | Permanently delete selected assets |
| Quarantine Selected | Move selected assets to `/Game/_Quarantine` for safe review before deletion |

> **Warning:** Deletion is permanent. Use Quarantine first if you are unsure whether an asset is truly unused.

---

## Known Limitations

- Assets only referenced via string paths (e.g. `LoadObject<T>` with hardcoded paths) may appear as unused even though they are needed at runtime.
- Assets used exclusively in C++ via hardcoded paths will not show inbound references in the Asset Registry.
- Always review the list carefully before bulk deleting.
