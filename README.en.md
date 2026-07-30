# Country Info Lookup

English | **[简体中文](./README.md)**

A pure front-end, single-file country / region information lookup tool. Just double-click `index.html` to use it — no installation, no back-end, and zero external dependencies.

## Features

- 🌐 **Multi-language UI**: Switch among 7 languages — Simplified Chinese, Traditional Chinese, English, Japanese, Korean, Thai, and Malay. Your language choice is saved automatically. Country names come from the official Unicode CLDR localized annotations.
- 🔍 **Multi-dimensional search**: Match by name (including aliases), English name, 2/3-letter country codes (CN / CHN), ISO numeric code (156), currency code (USD), currency name, dial code (+86 / 86), or top-level domain (.cn). Search adapts to the active language.
- 🗂️ **Continent grouping**: Browse by seven groups — Asia, Europe, North America, South America, Africa, Oceania, Antarctica.
- 🗺️ **World map view**: Switch between the country list and an interactive world map. Country areas are linked to built-in data: hover for a name, click to open details, use the controls to zoom, drag with two fingers to pan, or pinch to zoom.
- 📋 **Per-item copy**: The detail panel shows CCA2 / CCA3 / numeric code / top-level domain / dial code / official name / capital / language — each copyable with one click.
- 💱 **Currency info**: Currency code, symbol, and name, with a localized `Intl.NumberFormat` format example (e.g. ¥1,234.56).
- 🕐 **Time-zone current time**: Shows each country's IANA time zones with the current time and UTC offset, auto-refreshing every 30 seconds.
- ⭐ **Favorites + Recent**: Favorites and recently viewed are stored locally (`localStorage country-info-favs` / `country-info-recent`, capped at 24, de-duplicated and moved to front).
- 🌓 **Light / dark theme**: One-click toggle; the preference is saved in `localStorage country-info-theme`.
- 📱 **Responsive layout**: The detail panel sits on the right on desktop and slides to the bottom on mobile.

## Usage

Open `index.html` directly in your browser:

```bash
open index.html        # macOS
# or drag it into your browser
```

Type any keyword in the search box to filter; press `/` to focus the search box, `Esc` to clear the search or close the detail panel. Use the 🌐 button in the header to switch the interface language.

## Technical Notes

- A single HTML file built with native HTML / CSS / JavaScript — zero dependencies and zero build steps.
- Data is embedded as a JavaScript constant: country info from [mledoze/world-countries](https://github.com/mledoze/countries) (ODbL); timezone mapping from moment-timezone; 250 countries / regions in total.
- All parsing and rendering happen locally in the browser. No data is ever uploaded.
- Dynamic rendering always uses `createElement` / `textContent` to avoid XSS injection risks.
- Flags use the system Emoji font; Windows desktop does not support flag emoji, so they display as two-letter country codes (e.g. CN).

## Live Demo

Deployed via GitHub Pages and available here:

🔗 **https://blog.wangruofeng007.com/country-info/**

Source repository: https://github.com/wangruofeng/country-info
