# 10 - Scoped Policies, Inspector and Diagnostics

> Release preparation for Project Structure Guard v1.3.0, Unreal Engine 5.8. This version is not yet marked as publicly available on Fab.

## Scoped Project Policies

Global Naming Rules, Folder Rules, Excluded Paths and Protected Paths remain the fallback policy. In **Project Settings > Project Structure Guard**, scoped policies can override individual policy categories for specific `/Game/...` folder areas.

- More specific matching folder scopes take precedence over broader matching scopes.
- Each category is resolved independently: a child can override naming while inheriting folder rules and protection settings from its parent.
- An explicitly enabled empty override means that category is intentionally empty, not inherited.
- A scope that does not override a category inherits that category from its nearest applicable parent or the global policy.
- Exclusion and protection constraints also affect applicable validation and structural operations.

**Example:** A shared global naming policy can apply to most assets, while `/Game/UI` uses a different naming convention. Do not assume that changing a global rule also changes areas with their own naming override.

## Effective Policy Inspector

Open the **Inspector** tab to see what PSG would apply to one asset or internal folder path.

1. Enter an internal Unreal package/folder path, or use the supported Content Browser selection.
2. Inspect the matching scope chain and whether each category is **GLOBAL**, **INHERITED** or **OVERRIDDEN**.
3. Check the effective naming/folder rules, excluded/protected paths and the reasons for relevant exclusions/protection.
4. For a specific asset, compare the configured rules with the rules selected for that asset class.

The Inspector is an explanation tool. It does not rename, move, fix or validate assets as a separate compliance engine. Select one target at a time; ambiguous multi-selection is not silently reduced to one asset.

## Policy Diagnostics

Open **Policy Diagnostics**, then refresh after editing settings. These read-only diagnostics detect a limited set of configuration issues and explain their scope/rule indices, reasons and suggested manual corrections.

The diagnostics include codes `PSD001` through `PSD008` for issues such as missing or invalid scope paths, duplicate scopes, inert overrides and duplicate applicable rules. Results are **warnings or informational notes**, not an automatic settings repair or a substitute for project validation. A clean result does not prove that every convention is correct.

## Policy Impact Preview

In **Rules**, select exactly one *existing global* Naming Rule or Folder Rule and choose **Preview Toggle Impact**.

The preview hypothetically toggles that rule's Enabled state and compares findings using the existing scanner and policy resolution pipeline. Review **Findings before**, **Findings after**, **Added**, **No longer reported**, **Unchanged** and **Affected assets**. It may also identify a different first-matching rule on the same asset.

- The preview is **read-only**. It does not apply a toggle, change config, alter assets or update baselines.
- It covers only toggling one existing **global** naming or folder rule, not changing rule signatures, drafting new rules or editing scoped overrides.
- **No longer reported** does not mean the underlying asset was fixed; policy changes can change classification.
- Scope overrides may mean a global rule has no effect in some folder areas.

## Related Pages

- [Rule Manager](05_Rule_Manager.md)
- [Validation](03_Validation.md)
- [Baseline Review and Adoption](11_Baselines_Adoption.md)
- [Troubleshooting](08_Troubleshooting.md)
