# Unused Asset Scanner

The Unused Assets tab finds assets in your project that are **not referenced** by any other asset — maps, blueprints, materials, or anything else.

---

## How It Works

1. **Collects all assets** under `/Game/` from the Asset Registry
2. **Builds a dependency graph** using the Asset Registry's dependency data
3. **Collects root references** — all maps (`.umap`) and their full dependency trees via BFS traversal
4. **Marks as unused** any `/Game/` asset that is not reachable from any root

The BFS traversal follows dependencies through **all paths**, including engine and plugin references, ensuring that assets referenced indirectly (e.g. Material → Engine Material Function → your Texture) are correctly detected.

---

## Scanning

Open the PSG window and select the **Unused Assets** tab.

1. Click **Scan Unused Assets**
2. Results show all unreferenced assets, sorted by size (largest first)

Each result shows:

| Column | Description |
|---|---|
| **Asset** | Asset name |
| **Class** | Asset type (Blueprint, Material, Texture, etc.) |
| **Path** | Full package path |
| **Size** | Disk size of the asset |

The header displays total unused count and potential disk savings.

---

## Actions

### Move to Quarantine (Recommended)

The **safe default action**. Selected assets are moved to `/Game/_PSG_Quarantine/`, preserving their relative folder structure.

- Assets in quarantine are **excluded from all scans** (validation and unused)
- No data is deleted — you can manually move assets back if needed
- Redirectors are **not** created (the move is a package rename)

Use quarantine when you are not 100% certain an asset is truly unused.

### Delete Permanently

Permanently deletes the selected assets from disk. **This cannot be undone.**

Use this only for assets you are absolutely certain are not needed.

---

## What Counts as "Referenced"?

An asset is considered **referenced** (and will NOT appear in the unused list) if:

- It is a **map** (`.umap`) — maps are always root assets
- It is **directly or indirectly referenced** by any map
- It is referenced by another referenced asset (transitive)

An asset is considered **unused** if:

- No map or referenced asset depends on it
- It is not under an excluded path

---

## Excluded Paths

The following paths are always excluded from the unused asset scan:

- All paths listed in **Project Settings → Excluded Paths**
- `/Game/_PSG_Quarantine/` (automatically excluded)
- `/Game/Developers/` (if "Exclude Developer Folders" is enabled)
- `/Game/__ExternalActors__/`
- `/Game/__ExternalObjects__/`

---

## Tips

- **Scan regularly** — unused assets accumulate over time and waste disk space
- **Use quarantine first** — verify your project still works before permanently deleting
- **Multi-select** — hold `Ctrl` to select multiple assets for batch operations
- **Sort by size** — focus on the largest unused assets first for maximum savings
