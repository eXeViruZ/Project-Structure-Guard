# 06 — Unused Asset Cleanup

> This page describes **Project Structure Guard v1.2.0 for Unreal Engine 5.8**.

## Overview

The **Unused Assets** workflow helps identify project content with no tracked inbound references and provides a controlled cleanup path.

Project Structure Guard v1.2 emphasizes review and recovery instead of immediate destructive deletion:

1. Scan for unused candidates.
2. Review the results.
3. Move selected candidates into managed Quarantine.
4. Restore assets if they are needed again.
5. Use Permanent Delete only for managed quarantined content after the final safety checks pass.

---

## Scan Behavior

The scanner uses Unreal asset dependency/reference information to identify unused candidates.

The v1.2 workflow avoids mixing normal cleanup candidates with content that should not be treated as ordinary unused assets, including generated Blueprint artifacts, redirectors, and managed quarantine content.

A scan result is a cleanup candidate, not a guarantee that an asset is semantically unnecessary to your game or tool.

---

## Review Before Cleanup

Before moving anything to Quarantine, review:

- Asset name
- Asset class
- Package path
- Reference context available to the scanner
- Whether the asset may be loaded dynamically or referenced outside normal Asset Registry relationships

For projects that use hardcoded paths, string-based loading, custom external data, or other dynamic systems, additional manual verification may be necessary.

---

## Quarantine

Use the managed Quarantine workflow instead of immediately destroying ordinary project assets.

When an asset is quarantined, Project Structure Guard records the information required for its managed cleanup/recovery workflow.

Quarantine provides a review period before permanent deletion and keeps the destructive step separate from initial unused-asset detection.

---

## Restore from Quarantine

Managed quarantined assets can be restored to their recorded original locations.

Restore performs safety checks before moving the asset back. If the original destination is no longer safe or available, Project Structure Guard blocks the operation instead of blindly overwriting project content.

After restoring content, re-run relevant validation/reference checks as part of your normal review.

---

## Permanent Delete

**Permanent Delete is intentionally guarded in v1.2.0.**

Ordinary project assets cannot be directly permanently deleted through this workflow. Permanent Delete is available only for assets that are recognized as managed quarantined content and pass the required safety checks.

Project Structure Guard also checks for external referencers before allowing managed quarantined content to be permanently deleted.

If the safety contract is not satisfied, deletion is blocked.

> Permanent deletion is destructive. Quarantine and verify first.

---

## Known Limitations

No automated unused-asset scanner can infer every runtime usage pattern.

Assets may require additional manual review when they are used through mechanisms such as:

- Hardcoded string/package paths
- C++ loading logic not represented as normal tracked asset references
- External configuration or data-driven paths
- Custom runtime discovery systems

Always treat the unused scanner as a project-cleanup aid, not as proof that content can never be needed at runtime.

---

## Recommended Cleanup Workflow

1. Commit or back up the project.
2. Run the unused asset scan.
3. Review candidates carefully.
4. Quarantine only the assets you intend to investigate/remove.
5. Test the project after quarantine.
6. Restore anything that is still required.
7. Permanently delete only managed quarantined assets after the safety checks pass and you are confident they are no longer needed.
