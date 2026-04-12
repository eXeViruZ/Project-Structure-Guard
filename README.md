# Project Structure Guard

**Automated asset naming & folder validation for Unreal Engine 5.7+**

Project Structure Guard enforces consistent naming conventions and folder structures across your entire Unreal Engine project. It catches violations on save, provides one-click auto-fix, finds unused assets, and integrates into CI/CD pipelines via a commandlet.

---

## Features

- **Naming Validation** — Enforce prefixes (`BP_`, `M_`, `SM_`, etc.), suffixes, and casing rules per asset class
- **Folder Validation** — Ensure assets live under the correct base paths
- **On-Save Validation** — Real-time toast notifications when a saved asset violates a rule
- **Auto-Fix** — One-click rename and move for all fixable violations
- **Unused Asset Scanner** — Find unreferenced assets with BFS dependency analysis, quarantine or delete them safely
- **CI/CD Commandlet** — Run validation headlessly from the command line with JSON/CSV reports and configurable exit codes
- **Built-in Presets** — Epic Official, Allar Style Guide, and Lyra rule sets out of the box
- **Rule Sharing** — Export/Import rules as JSON files for team-wide consistency
- **CSV Reports** — Export scan results for review or archiving

---

## Quick Start

1. Install the plugin into your project's `Plugins/` folder
2. Enable it in **Edit → Plugins → Project Structure Guard**
3. Open **Edit → Project Settings → Project → Project Structure Guard**
4. Load a preset (Epic Official, Allar, or Lyra) or configure your own rules
5. Open the PSG window: **Tools → Project Structure Guard**
6. Click **Scan Whole Project** — review and fix violations

For detailed setup, see [Getting Started](docs/getting-started.md).

---

## Documentation

| Page | Description |
|---|---|
| [Getting Started](docs/getting-started.md) | Installation, first scan, and Project Settings |
| [Validation](docs/validation.md) | Naming rules, folder rules, on-save validation, auto-fix |
| [Unused Assets](docs/unused-assets.md) | Scanner, quarantine, delete, BFS dependency analysis |
| [Commandlet (CI/CD)](docs/commandlet.md) | Headless validation, flags, JSON/CSV reports, exit codes |
| [Rule Presets](docs/rule-presets.md) | Built-in presets, custom rules, Export/Import JSON |
| [FAQ](docs/faq.md) | Common questions and troubleshooting |

---

## Supported Engine Versions

| Engine Version | Status |
|---|---|
| UE 5.7 | Fully Supported |

---

## Support

- **Discord:** [Hanke Unreal Tools](https://discord.gg/vgpmnN6nCR)
- **GitHub Issues:** [eXeViruZ/Project-Structure-Guard](https://github.com/eXeViruZ/Project-Structure-Guard/issues)

---

## License

MIT License — see [LICENSE](LICENSE) for details.

© 2026 Tom Leon Vincent Hanke
