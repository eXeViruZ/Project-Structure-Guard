# 08 — Troubleshooting

> This page describes **Project Structure Guard v1.2.0 for Unreal Engine 5.8**.

---

## Project Structure Guard does not appear in the Tools menu

**Possible cause:** The plugin is not enabled or the installed package does not match the Unreal Engine version.

**Check:**

1. Go to **Edit → Plugins**.
2. Search for **Project Structure Guard**.
3. Confirm the plugin is enabled.
4. Confirm you are using **v1.2.0 with UE 5.8** or the earlier **v1.1.1 with UE 5.7**.
5. Restart the editor if required.

---

## No validation results appear

**Possible causes:**

- No applicable naming/folder rules are configured.
- Relevant rules are disabled.
- The selected scan scope contains no matching violations.
- Search or filters currently hide the findings.

**Check:**

1. Clear Validation Results Search.
2. Reset or review the active filters.
3. Confirm at least one naming or folder rule is enabled.
4. Run **Scan Whole Project** as a broader comparison.
5. Review the Rule Manager if a preset/import recently changed the active configuration.

---

## A validation finding disappears when I search or filter

Search and filters are part of the same active filtering pipeline.

If the currently selected finding no longer matches the active Search/filters, its selection is cleared to avoid showing stale hidden Result Details.

Clear or adjust Search/filters to show the finding again.

---

## Fix or Move is blocked

Project Structure Guard blocks structural operations when the preflight safety contract is not satisfied.

Common causes include:

- The destination already exists.
- Multiple operations target the same destination.
- The asset is under a Protected Path.
- The finding is not fixable by the selected operation.
- Another preflight condition marks the operation as Blocked, Skipped, or Conflict.

Open the relevant preview and review the displayed state and block reason instead of forcing the operation.

---

## A protected asset still appears as a violation

This is expected.

**Protected Paths do not hide validation problems.** They keep findings visible while blocking supported rename, move, and applicable auto-fix operations that would modify protected content.

Use the Result Details/preview information to confirm the Protected state and block reason.

---

## `-failonnew` fails CI even though known issues were accepted

Check the baseline configuration first.

1. Confirm the expected baseline exists and is loaded.
2. Confirm the configured project-relative baseline path is correct for the CI workspace.
3. Confirm the baseline file is present in source control if CI depends on it.
4. Review the generated CSV/JSON report and commandlet log to identify which findings are classified as **New**.
5. If the accepted project state intentionally changed, update the baseline in the editor and commit that change through the normal review process.

A non-zero commandlet result from `-failonnew` is an expected policy failure when New findings are present; it is not automatically an internal commandlet error.

---

## Baseline state is not what I expect

Baseline classification depends on the current baseline data and the current validation findings.

Check:

- Whether the intended baseline is loaded.
- Whether the baseline was updated or cleared recently.
- Whether rule configuration changed after the baseline was created.
- Whether the affected issue now has a different rule/issue identity because the project configuration changed.

Use baseline status and the Advanced Details fields when diagnosing identity-related differences.

---

## An unused asset cannot be permanently deleted

This is expected when the v1.2 deletion safety contract is not satisfied.

Ordinary project assets are not directly permanently deleted through the unused-asset workflow. Permanent Delete is restricted to **managed quarantined content** that passes the required safety checks.

Deletion can also be blocked when external referencers are detected.

Use Quarantine first, verify the project, then permanently delete only eligible managed quarantined assets.

---

## Restore from Quarantine is blocked

Restore is blocked when returning the managed quarantined asset to its recorded original location would not be safe.

Common examples include a destination conflict or other invalid destination condition.

Resolve the conflicting project state and retry instead of overwriting content.

---

## Unused scanner reports an asset that is needed at runtime

Automated reference analysis cannot infer every dynamic runtime usage pattern.

Review assets carefully if your project uses:

- Hardcoded package/string paths
- C++ loading logic not represented as normal tracked references
- External configuration/data-driven paths
- Custom runtime discovery systems

Restore the asset if it was quarantined and keep it out of destructive cleanup.

---

## Commandlet reports an internal error

Check:

1. The `.uproject` path is correct.
2. The command uses the UE 5.8 executable for PSG v1.2.0.
3. Any `-scanpath=` value uses a valid Unreal package path such as `/Game/...`.
4. Output directories/paths are valid and writable.
5. The commandlet log for the first concrete error before the final exit result.

Distinguish internal errors from expected policy failures caused by `-failonerror`, `-failonwarning`, or `-failonnew`.

---

## Support

If the issue is not covered here:

- Discord: https://discord.gg/vgpmnN6nCR
- GitHub Issues: https://github.com/eXeViruZ/Project-Structure-Guard/issues
