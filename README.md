# Steam PowerPlus

**Steam Store enhancements, without replacing Steam.**

[![Version](https://img.shields.io/badge/version-2.0.0-386b8b)](https://github.com/colmlenehan-gh/SteamPowerPlus/releases)
[![Status](https://img.shields.io/badge/status-development%20preview-bb8538)](https://github.com/colmlenehan-gh/SteamPowerPlus/releases)
[![License: CC0 1.0](https://img.shields.io/badge/license-CC0%201.0-596776)](LICENSE)

**Developed by Advanced** (formerly ACE Productions, Advanced Computing for Entertainment).  
**Repository:** https://github.com/colmlenehan-gh/SteamPowerPlus  
**Current version:** 2.0.0  
**Supported target:** https://store.steampowered.com/  
**Platform:** desktop browsers using Tampermonkey, with Google Chrome the primary target.

> [!IMPORTANT]
> **Development preview, not a verified stable release.** The userscript builds, passes JavaScript syntax validation, and has six passing automated tests. Live Steam browsing, Tampermonkey ZIP import, and cross-browser behavior have not yet been verified end to end. Please report issues rather than assuming all integration points work on current Steam pages.

Steam PowerPlus is an independent userscript that enhances the official Steam Store with personal browsing tools, optional page cleanups, additional game information, presentation controls, and a centralized settings interface. It is **not made by, affiliated with, endorsed by, or supported by Valve Corporation**.

## Contents

- [Features](#features)
- [Installation](#installation)
- [Getting started](#getting-started)
- [Settings and storage](#settings-and-storage)
- [Compatibility](#compatibility)
- [Privacy and security](#privacy-and-security)
- [Known limitations](#known-limitations)
- [Troubleshooting](#troubleshooting)
- [Development](#development)
- [Testing](#testing)
- [Releases and roadmap](#releases-and-roadmap)
- [Contributing and reporting bugs](#contributing-and-reporting-bugs)
- [License and credits](#license-and-credits)

## Features

The following capabilities are **implemented in the 2.0.0 source**, but their operation on live Steam pages has not yet been comprehensively validated.

| Area | Capability | Notes |
| --- | --- | --- |
| Control centre | PowerPlus navigation entry, accessible settings dialog, sidebar, overview and diagnostics | Fallback launcher may appear on unsupported navigation layouts. |
| Themes | Steam Enhanced, OLED Black, Classic Steam, Windows Aero, macOS-Inspired, Minimal Light, Midnight Blue and Custom | Themes style the **PowerPlus interface**, not all of Steam. |
| Appearance | Accent colour, density and corner-radius preferences | Theme options are intentionally limited in this preview. |
| Store cleanup | Optional removal of selected promotional, curator and announcement sections | Disabled by default; selection depends on page markup. |
| Game information | Show details available on an individual game's Steam page | Uses visible Steam content; may be absent on unsupported layouts. |
| Prices | Read visible prices and provide direct SteamDB links | No historical-price API or fabricated price history. |
| Gameplay discovery | Searches for gameplay, no-commentary footage, reviews, benchmarks, Steam Deck footage and beginner guides | Opens third-party searches only at the user's request. |
| Trailers | Autoplay, mute, volume and viewport-related preferences | Applies to supported HTML5 video elements, not every Steam player type. |
| Reviews | Reversible presentation enhancements | Not an authenticated friend-review or advanced filtering engine. |
| Artwork | Brightness, contrast, saturation and grayscale adjustments | Does not yet replace artwork through SteamGridDB. |
| Personal notes | Save notes for individual games | Local to Tampermonkey storage. |
| Discovery bookmarks | Save games separately from Steam's official wishlist | Does not edit your Steam wishlist. |
| Recently viewed | Optional local visited-game history | Off by default. |
| Comparison collection | Collect up to four games | A full side-by-side comparison table is **not** implemented. |
| Search helpers | Shortcuts for supported Steam search layouts | Availability depends on Steam page structure. |
| Configuration | Feature toggles, JSON import/export and reset controls | Review exports before sharing: they may contain private notes and history. |
| Shortcuts | `Alt+Shift+P` and `Alt+Shift+W` | Can conflict with host/browser shortcuts; configurable shortcut remapping is not implemented. |

Every feature is designed to be opt-in or independently toggleable where practical. If Steam changes a page layout, a feature might not attach correctly; this preview does not guarantee full reversibility in every live DOM state.

## Installation

### Option A: standalone userscript (recommended)

1. Install **[Tampermonkey from the Chrome Web Store](https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)**.
2. Visit `chrome://extensions/` in Chrome, select **Tampermonkey → Details**, and enable **Allow User Scripts** when available. Follow any additional requirements displayed by the installed Tampermonkey version. Developer Mode may be required in some configurations.
3. Download **`steampowerplus.user.js`** from the [GitHub Releases page](https://github.com/colmlenehan-gh/SteamPowerPlus/releases).
4. In Tampermonkey, open **Dashboard → Create a new script**. Replace the generated template with the downloaded userscript's full contents and save. Alternatively, use a supported direct `.user.js` installation route.
5. Open or reload **https://store.steampowered.com/**.
6. Find the **PowerPlus** navigation control or use the Tampermonkey menu command to open settings.

> [!NOTE]
> Installation does not require Node.js, Git, a server or a Steam password.

### Option B: ZIP import (unverified)

1. Download **`steampowerplus.zip`** from [Releases](https://github.com/colmlenehan-gh/SteamPowerPlus/releases).
2. Open **Tampermonkey → Dashboard → Utilities**.
3. Locate the option to import from a file and select `steampowerplus.zip`.
4. If Tampermonkey recognises the archive, review the script and approve the import.
5. Reload the Steam Store and check whether PowerPlus appears.

**Important:** The archive contains `steampowerplus.user.js` at its root, but acceptance by Tampermonkey's ZIP importer has **not** been tested. Tampermonkey's ZIP backup format may require additional metadata. If the import is rejected, use Option A. The source-code ZIP is not the same as the installation ZIP.

## Getting started

Open **PowerPlus** from the Steam Store navigation. The settings window groups available controls into sections for features, appearance, media and artwork, data, diagnostics, and product information.

Suggested first setup:

1. Keep cleanup off initially and confirm that the Steam Store behaves normally.
2. Select a theme for the PowerPlus interface.
3. Enable only the enhancements you need.
4. Open an individual game page to try notes, bookmarks, price links or gameplay searches.
5. Visit diagnostics if an enhancement fails to appear or throws an error.

Steam PowerPlus intentionally does not replace Steam's checkout flow, user account interface or purchasing functions.

## Settings and storage

Preferences use Tampermonkey's `GM_getValue` and `GM_setValue` APIs. The settings and local game data are stored under separate persistent storage keys. The script validates key configuration values when loading them.

- **Export:** Save configuration and local data as JSON for backup or transfer.
- **Import:** Load a previously exported configuration. Import only JSON files from sources you trust.
- **Reset:** Restore default settings or clear local data using the available controls.
- **Local data:** Notes, bookmarks, comparison entries and optional history are not synchronised with Steam or other browsers.

**Privacy warning:** A JSON backup can include your notes, saved games and browsing history. Do not upload it publicly or attach it to an issue report without reviewing its contents first.

## Compatibility

| Environment | Status |
| --- | --- |
| Google Chrome + Tampermonkey | Primary design target; not live integration-tested |
| Microsoft Edge + Tampermonkey | Potentially compatible; unverified |
| Firefox + Tampermonkey | Potentially compatible; unverified |
| Steam Store homepage | Intended integration; unverified live |
| Individual game pages | Implemented page-specific features; unverified live |
| Steam search results | Implemented helpers; layout-dependent |
| Wishlist, publisher and promotional pages | Limited or no dedicated functionality; unverified |
| Steam desktop application | Not supported as a native modification |
| Windows/macOS desktop PowerPlus applications | Not available |

The userscript matches `https://store.steampowered.com/*` only. Steam markup varies by region, login status, user preferences and page type. Not every feature appears everywhere.

## Privacy and security

Steam PowerPlus 2.0 is designed to minimise permissions and external access:

- Uses `GM_getValue`, `GM_setValue` and `GM_registerMenuCommand`.
- Does not request `GM_xmlhttpRequest`, `GM_cookie`, or an `@connect` allowlist.
- Does not collect Steam passwords, export Steam cookies, automate purchases or change account balances.
- Does not include third-party runtime JavaScript dependencies or analytics/telemetry services.
- Reads relevant information from Steam's currently displayed page; external links to SteamDB and YouTube are initiated by the user.
- Constructs UI text without assigning untrusted page content to `innerHTML`.

**External destinations:** `steamdb.info` for manually opened game information/price-history pages; `youtube.com` for manually opened gameplay searches. Steam PowerPlus does not claim to retrieve SteamDB historical pricing.

This is not a formal external security audit. Users should inspect userscript permissions and review updates before installing.

## Known limitations

The following are **not complete** in 2.0.0:

- Authenticated advanced wishlist management, discount sorting and wishlist caching.
- Actual price-history retrieval or dependable multi-region price comparisons.
- SteamGridDB API integration and user-provided artwork replacements.
- Developer/publisher catalogue aggregation using verified service data.
- Comprehensive metadata-based store filtering and saved filter profiles.
- Full side-by-side comparison of games and their specifications.
- Steam-wide theme overrides, fully custom CSS variables, searchable settings and configurable shortcut binding.
- Per-feature reset and full version-to-version migration coverage.
- Accessibility verification against WCAG 2.2 AA, browser E2E tests and performance profiling.
- Verified Tampermonkey ZIP import and integration on every supported Steam Store page.

Some enhancements depend on current CSS selectors and visible page data. Missing or changed markup may cause a module to hide itself or fail; see diagnostics and file an issue with reproducible steps.

## Troubleshooting

**PowerPlus does not appear:** Confirm that Tampermonkey is installed and enabled, the script is switched on, Chrome permits user scripts where needed, and you are on `https://store.steampowered.com/`. Refresh the page. Check the userscript menu command if the navigation button is absent.

**A feature is not displayed:** Some modules only run on individual game pages or search pages. Ensure its toggle is enabled and open the diagnostics section. Steam may have changed its layout.

**ZIP cannot be imported:** Use the standalone `.user.js` installation method. ZIP import has not been live-verified.

**Settings were lost or reset:** Check whether Tampermonkey data was cleared or another browser profile is in use. Restore your own JSON backup when available.

**Report a defect:** Include the PowerPlus version, browser version, Tampermonkey version, operating system, affected Steam URL, expected behavior, observed behavior and reproducible steps. Remove any sensitive information from logs or screenshots.

## Development

The compiled userscript is standalone. Contributors need **Node.js 20 or later** to run the local build and test commands.

```bash
git clone https://github.com/colmlenehan-gh/SteamPowerPlus.git
cd SteamPowerPlus
npm run build
npm test
npm run check
```

`npm run build` generates `dist/steampowerplus.user.js`. `npm test` runs Node's built-in test runner. `npm run check` builds the script, checks JavaScript syntax and executes the tests.

Project layout:

```text
Steam-PowerPlus/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── SECURITY.md
├── TEST-RESULTS.md
├── package.json
├── src/
│   └── main.js
├── tests/
├── scripts/
│   └── build.mjs
├── dist/
│   └── steampowerplus.user.js
└── releases/
    └── steampowerplus.zip
```

Although modules are organised within the userscript, the initial 2.0 build is **not yet split into separate source files per module**. That refactor remains on the roadmap.

## Testing

The accompanying `TEST-RESULTS.md` reports the checks executed for the initial 2.0.0 build on **27 October 2026**:

| Check | Reported result |
| --- | --- |
| Build | Passed |
| JavaScript syntax validation | Passed |
| Automated tests | 6 passed, 0 failed |
| Settings validation | Passed selected unit checks |
| Module lifecycle idempotency | Passed selected unit check |
| Metadata/static safety checks | Passed selected source checks |
| Archive contents/readability | Inspected programmatically |
| Live Steam browser integration | Not tested |
| Tampermonkey ZIP import | Not verified |
| Accessibility/performance/browser matrix | Not tested |

These results relate to the local development build; they do **not** establish production reliability. Rerun the checks for any new source changes.

## Releases and roadmap

- **2.0.0 (27 October 2026):** Ground-up development-preview rebuild; new settings experience, UI themes, reversible page enhancements, local game collections and initial automated tests.

For assets and release notes, see [GitHub Releases](https://github.com/colmlenehan-gh/SteamPowerPlus/releases). The roadmap prioritises real-browser verification, installation testing, robust DOM fixtures, accessibility work, improvements to module separation and, only where reliable sources exist, further data-backed features.

Potential future Windows and macOS applications are **not part of this release**.

## Contributing and reporting bugs

Code and documentation contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) and [SECURITY.md](SECURITY.md).

- **Issues and feature requests:** https://github.com/colmlenehan-gh/SteamPowerPlus/issues
- **Bug reports/security contact:** ok.hey.services@gmail.com

For security reports, avoid publicly disclosing sensitive exploit details before maintainers can evaluate them. Never send account passwords, Steam tokens or cookies.

## License and credits

**Steam PowerPlus is dedicated under [CC0 1.0 Universal](LICENSE).** To the extent permitted by law, you may copy, modify, distribute and use its original code, including commercially, **without an attribution requirement**. CC0 does not grant rights to Steam trademarks, artwork or other third-party content.

**Developer and maintainer:** Advanced (formerly ACE Productions, Advanced Computing for Entertainment).  
**Official repository:** https://github.com/colmlenehan-gh/SteamPowerPlus

Steam and related trademarks belong to Valve Corporation. SteamDB and YouTube are third-party services and are not project partners or endorsers.
