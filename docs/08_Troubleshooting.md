# 08 — Troubleshooting

---

## PSG window does not appear in the Tools menu

**Cause:** Plugin is not enabled.

**Fix:**
1. Go to **Edit → Plugins**.
2. Search for **Project Structure Guard**.
3. Enable the checkbox and restart the editor.

---

## No results after scan

**Cause:** No naming or folder rules are configured, or all rules are disabled.

**Fix:**
1. Go to **Edit → Project Settings → Project Structure Guard**.
2. Check that at least one Naming Rule or Folder Rule exists and is enabled.
3. Alternatively, load a preset via the **Presets** menu in the PSG toolbar.

---

## Fix All Safe renames 0 assets

**Cause:** No results are auto-fixable, or all auto-fixable results are filtered out.

**Fix:**
1. Make sure the **Auto-fixable only** filter is off, or check filtered results.
2. Check that the affected rules have a clear single prefix defined — ambiguous rules are skipped.

---

## Asset is blocked after Fix All Safe

**Cause:** The asset matches more than one naming rule, making the correct fix ambiguous.

**Fix:** Check your naming rules in Project Settings and ensure each asset class is covered by at most one naming rule with a unique prefix.

---

## Move All Safe moves 0 assets

**Cause:** No folder violations are auto-fixable, or the required folder path in the rule is missing.

**Fix:** Check Folder Rules in Project Settings and ensure each rule has a valid `/Game/...` package path set.

---

## Commandlet exits with code 2

**Cause:** Internal error during validation — usually a missing project file path or invalid scan path.

**Fix:**
1. Verify the `.uproject` path passed to the commandlet is correct and absolute.
2. Verify `-scanpath=` starts with `/Game`.
3. Check the commandlet log output for the specific error message.

---

## On-Save validation fires on every save even for clean assets

**Cause:** A rule with a very broad asset class (e.g. `Object`) is matching everything.

**Fix:** Review your naming rules and narrow the Asset Class field to specific types.

---

## Support

If your issue is not listed here:

- Discord: https://discord.gg/vgpmnN6nCR
- GitHub Issues: https://github.com/eXeViruZ/Project-Structure-Guard/issues
