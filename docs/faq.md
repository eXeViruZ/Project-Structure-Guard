# FAQ

## General

### Where are settings stored?

Settings are stored in `Config/DefaultProjectStructureGuard.ini` and are version-controlled with your project. This means all team members share the same rules.

### Does PSG modify my assets automatically?

No — PSG never modifies assets without explicit user action. Scanning is read-only. Auto-fix (rename/move) only happens when you click **Fix Selected**, **Fix All Safe**, **Move Selected**, or **Move All Safe**.

### Does PSG work with World Partition?

Yes. External actors (`__ExternalActors__`) and external objects (`__ExternalObjects__`) are automatically excluded from scanning.

### Does PSG affect runtime performance?

No. PSG is an **editor-only** plugin. It is not included in packaged builds and has zero runtime overhead.

---

## Unused Asset Scanner

### How does PSG determine if an asset is unused?

PSG uses the Asset Registry's dependency data to build a full dependency graph. Starting from all maps (`.umap`) in your project, it traverses the entire dependency tree via BFS. Any `/Game/` asset not reachable from any map is considered unused.

### Will PSG flag assets used only in code (C++ soft references)?

If an asset is referenced via `FSoftObjectPath` or `TSoftObjectPtr` **and** the reference is stored in a Blueprint default or a Data Asset, PSG will detect it. Pure C++ string references that are not serialized in any asset will **not** be detected — these assets may appear as false positives.

### What is the Quarantine folder?

`/Game/_PSG_Quarantine/` is a safe holding area for potentially unused assets. Assets moved there:
- Are excluded from all future scans
- Keep their original relative folder structure
- Can be manually moved back if needed

### Can I undo a permanent delete?

No. **Delete Permanently** removes the asset from disk. Use **Move to Quarantine** if you are not certain.

---

## Validation

### What does "first matching rule wins" mean?

Naming rules are checked top-to-bottom. Once a rule matches the asset's class name, that rule is used and no further rules are checked. This means:
- Put specific rules (e.g. `MaterialInstanceConstant` → `MI_`) **above** general rules (e.g. `Material` → `M_`)
- A catch-all rule (empty class name) should be the **last** rule

### Why does my asset show a folder violation after quarantine?

It shouldn't — quarantined assets are automatically excluded from all scans. If you see this, make sure you are running the latest version of the plugin.

### What happens to redirectors after rename/move?

Unreal creates Object Redirectors when assets are renamed or moved. Click **Cleanup Redirectors** in the PSG window to fix them up. This is a standard UE operation and is safe to run at any time.

---

## Commandlet

### Can I run the commandlet without opening the editor?

Yes — the commandlet runs in headless mode via `UnrealEditor-Cmd.exe`. No editor window is opened.

### How do I fail a CI build on violations?

Use `-failonerror` to fail on errors only, or `-failonwarning` to fail on any issue. Both return exit code `1` when violations are found.

### Where is the default CSV report written?

If no `-outputcsv` or `-outputjson` flag is specified, a CSV report is automatically written to `Saved/PSGReports/PSG_Report_YYYYMMDD_HHMMSS.csv`.

### Can I scan only a specific folder from the commandlet?

Yes — use `-scanpath=/Game/MyFolder` to limit the scan scope.

---

## Troubleshooting

### "No rules configured" warning

You have no naming or folder rules set up. Load a preset or add rules in Project Settings.

### Assets are not appearing in scan results

Check if the asset's path is listed in **Excluded Paths** in Project Settings. Also verify that "Exclude Developer Folders" is not hiding the asset.

### Commandlet shows different results than the editor

Make sure you have saved all assets and your project settings before running the commandlet. The commandlet reads from the saved Asset Registry cache, not the live editor state.

---

## Support

- **Discord:** [Project Structure Guard](https://discord.gg/wWtgwd9APR)
- **GitHub Issues:** [eXeViruZ/Project-Structure-Guard](https://github.com/eXeViruZ/Project-Structure-Guard/issues)
