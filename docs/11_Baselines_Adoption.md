# 11 - Baseline Review, Manual Reconciliation and Adoption

> Release preparation for Project Structure Guard v1.3.0, Unreal Engine 5.8. v1.3.0 is not yet publicly released on Fab.

## What a Baseline Means

A baseline records the findings accepted for tracking at a particular time. It does not fix the assets or guarantee that past violations have been corrected.

- **New:** A finding not matched to the stored baseline.
- **Existing:** A finding matched to a stored baseline entry.
- **Unclassified:** No applicable baseline classification.
- **Resolved:** A historical comparison label meaning the stored identity was not found in the compared scan. **It is not proof of remediation.**

Rule changes, renames and moves can change issue identities. A finding missing from a partial scan is especially **not** proof that it has been resolved.

## Create, Update and Clear

In **Validation**, after an appropriate scan:

- **Create Baseline:** Establishes the initial baseline **only if the configured file is missing**. This action does not overwrite an existing file.
- **Update Baseline:** A separate, explicitly initiated workflow for changing the accepted baseline. Review what it will add/remove before confirming; this can accept new findings.
- **Clear Baseline:** A separate destructive baseline-management action. Back up or commit the baseline first.

Configure the **project-relative baseline path** in Project Settings. For team workflows, review and commit baseline and policy changes together.

## Review Baseline

Run **Scan Whole Project** and choose **Review Baseline** in Validation. Review the counts for **Stored**, **Existing**, **New**, **Unmatched**, **Held/Uncertain** and **Verified removable**, plus the policy-freshness status.

**Unmatched** means a stored entry did not match the current comparison. **Held/Uncertain** communicates why PSG cannot conclude it was genuinely fixed. Automatic verification of removable old entries is not promised.

A partial, stale or missing scan is not sufficient authorization to remove baseline entries.

## Remove Selected Baseline Entries

For a current **Whole Project** scan with eligible unmatched entries:

1. Inspect individual unmatched entries and their hold reasons.
2. Select only the specific entries you intend to remove. Nothing is selected automatically.
3. Preview the selected removal and inspect the entry identities and warning.
4. Use **Remove Selected Baseline Entries** and explicitly confirm.
5. Review the resulting baseline and run validation again.

This operation removes **only the selected stored entries** when its safety checks pass. It does **not** delete, rename or fix assets and does **not** implicitly accept new findings. If the baseline file, settings, scan, selection or policy becomes stale, the operation is blocked. Recovery/staging files or write failures can also block protected operations.

The normal **Update Baseline** workflow is different: it can accept new findings and must be used consciously.

## Adopt Project

Use the **Adopt Project** tab when introducing PSG to an existing project:

1. **Scan Project:** Start a fresh whole-project scan.
2. **Review Findings:** Inspect counts and the breakdown by folder area.
3. **Understand Baseline Status:** Check the configured path, existing baseline and any unresolved recovery/staging artifacts.
4. **Choose the Next Action:** Where eligible, explicitly create a missing initial baseline; otherwise evaluate the existing baseline or continue without creating one.

Reviewing and scanning do not change assets. **Create Initial Baseline** requires an explicit confirmation and will not overwrite an existing baseline. A missing/invalid baseline path, stale scan or unresolved artifact can prevent creation.

### Filesystem limitation

The **initial baseline creation** path in Adopt Project currently requires a supported local Windows physical filesystem. On Mac/Linux and unsupported sandbox or network filesystem paths it is restricted. Other supported read-only inspection and validation workflows are separate from that creation operation.

## Recommended Team Practice

Back up or commit the original rules and baseline before changing their meaning. Review scoped rules, issue identities and each proposed baseline change in code review. Do not interpret removed or unmatched entries as repaired project content.

## Related Pages

- [Validation](03_Validation.md)
- [Scoped Policies and Inspector](10_Policies_Inspector_Diagnostics.md)
- [CI/CD Commandlet](07_Commandlet.md)
- [Troubleshooting](08_Troubleshooting.md)
