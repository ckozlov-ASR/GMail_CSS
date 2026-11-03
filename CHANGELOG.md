# Changelog

All notable changes to this theme are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and versions follow
[Semantic Versioning](https://semver.org/).

## [Unreleased]

### Changed
- **New name: GMail Swatches.** The project, README and style
  descriptions use the new name, and each theme is now called a swatch.
  Style `@name`s are unchanged, so pasting an update over an installed
  style still works.
- **Softer thread header.** The sender/date strip on each message in a
  thread now uses a pale tint of the theme color instead of the full accent,
  with a thin accent-colored line underneath, so the sender and date are
  easier to read. Set by the new `--gm-thread-header` variable in each
  theme; themes without it fall back to the full accent.
- **Rounded selected label.** The selected sidebar label (e.g. Inbox) has
  a rounded right end again, matching the shape of a hovered label.
- **Plain-English settings notes.** Every color in the themes and every
  shape, size and speed setting in the base now has a note saying what it
  changes and a suggested range (e.g. "Strength: 0.10 lighter … 0.30
  darker"), plus a short "how to change colors" guide at the top of each
  theme, so no CSS knowledge is needed to adjust them.

### Added
- **New base settings:** `--gm-label-radius` (sidebar folder rounding, also
  applied to hovered folders), `--gm-row-height` (inbox row height) and
  `--gm-label-font-size` (sidebar text size), replacing fixed values.

## [3.0.0] — 2026-11-02 — Base + themes

Breaking: the single Autumn file is split into a layout base plus theme
files. Existing Stylus styles need replacing (see **Upgrading** below).

### Changed
- **Layout and colors split.** `Gmail_base.css` holds all the layout,
  shapes and spacing and sets no palette. Each color scheme is now a short
  file in `themes/`: `autumn.css`, `ocean.css` and `ember.css`.
- **Autumn is now per-account too.** Like Ocean and Ember it applies to one
  account matched by email address, instead of every account. Accounts
  without a theme get the base's neutral grays; change a theme's selector
  to `:root` to make it the default.
- **Variables renamed by role**, replacing names left over from the green
  theme:
  - `--gm-green` → `--gm-hover-soft`
  - `--gm-green-strong` → `--gm-hover`
  - `--gm-gray-selected` → `--gm-label-selected`
  - `--gm-blue-link` → `--gm-label-text`
  - `--gm-blue-unread` → `--gm-row-unread`
  - `--gm-white-read` → `--gm-row-read`
  - `--gm-yellow-selected` → `--gm-accent`
- **Neutral fallbacks.** Every color in the base has a gray fallback, so
  Gmail still looks reasonable with no theme installed.
- README rewritten around the base + themes layout, with a variable
  reference and steps for adding a theme.

### Removed
- `Gmail_autumn.css`, `Gmail_palette_ocean.css` and
  `Gmail_palette_ember.css` (still available at tag `v2.3.0`).

### Upgrading
1. Add `Gmail_base.css` as a new Stylus style (it's named **Base Gmail
   CSS**).
2. Paste `themes/autumn.css` over **Gmail Autumn**, `themes/ocean.css` over
   **Gmail Ocean** and `themes/ember.css` over **Gmail Ember**, then put
   each account's email address in (Autumn now needs one too).

## [2.3.0] — 2026-11-02 — Bolder subjects, Stylus headers

### Changed
- **Bolder subject lines.** Read-message subjects go from normal (400) to
  500, and unread subjects from 500 to 600, so unread stays heavier than
  read.
- **Stylus headers.** `Gmail_autumn.css` and `Gmail_palette_ocean.css` now
  start with a `==UserStyle==` header ("Gmail Autumn", "Gmail Ocean") and
  wrap their rules in `@-moz-document domain("mail.google.com")`, like the
  Ember file.

### Fixed
- Pasting the Autumn or Ocean file into a Stylus UserCSS style no longer
  fails with "Could not find metadata" or the @name/@namespace clash.

## [2.2.0] — 2026-11-02 — Ember palette

### Added
- **Ember palette** (`Gmail_palette_ember.css`): copper hovers, a rust
  selected label with dark espresso text, peach unread rows, cream read rows
  and flame-orange highlights, matched to a dark chocolate-and-copper Gmail
  background. Applies to one Gmail account, like the Ocean palette.
- The Ember file includes a Stylus `==UserStyle==` header and an
  `@-moz-document` block, so pasting it into Stylus no longer triggers the
  "change the value of @name or @namespace" error.

## [2.1.0] — 2026-11-02 — Ocean palette

### Added
- **Ocean palette** (`Gmail_palette_ocean.css`): sky blue, slate, pale aqua
  and seafoam colors with a deep navy selected-label link, applied on top of
  the Autumn theme for a single Gmail account, matched by the email address
  in the account avatar's `aria-label`.
- README section on giving each Gmail account its own colors, including the
  separate-browser-profile setup.

## [2.0.0] — 2026-11-02 — Autumn theme

A full restyle of the green theme around a warm autumn palette, plus two new
styled areas.

### Changed
- **Palette.** Replaced the green/blue/gray scheme with autumn colors:
  - unread rows: soft blue → warm cream
  - read rows: translucent white → warm off-white (`#faf8f2`)
  - selected rows: pale yellow → golden amber
  - selected sidebar label: light gray (`#E5E5E5`) → warm taupe (`#a89a7a`)
  - scrollbar, Compose hover and all hover states: bright green → sage
- **Theming.** All repeated values (colors, corner radius, font stack,
  transition) now live in CSS custom properties in `:root`, so the palette
  can be retuned in one place.
- **Sidebar shape.** The selected and hovered label rows keep Gmail's default
  shape instead of the custom 14px rounding.
- **Font stack.** Added a generic `sans-serif` fallback after Segoe UI and
  Open Sans.
- **Cleanup.** Merged the separate unread/read hover rules and the selected
  row/selected-hover rules into shared selectors; rewrote comments to explain
  what each Gmail class targets and why each override is needed.
- **File name.** `Gmail1_green.css` is now `Gmail_autumn.css`.

### Added
- **Category tabs.** The active Primary/Promotions/Updates tab gets an amber
  background with rounded top corners and a sage underline; inactive tabs
  turn sage on hover.
- **Thread view.** Each message in a conversation, expanded or collapsed, is
  drawn as a rounded card with a soft shadow; expanded messages get an amber
  sender/date header strip and tighter spacing below it.
- **Hover transitions.** Background colors ease in over 0.15s instead of
  snapping.

### Fixed
- Sidebar folder icons and label text looked faded because Gmail lays a
  translucent white wash (`rgba(255,255,255,0.3)`) over each label. The label
  background is now transparent, so icons render at full strength and the
  selected/hover colors show cleanly.

### Removed
- `Gmail1_green.css` (still available at tag `v1.0.0`).

## [1.0.0] — 2026-04-18 — Green theme

First published version.

### Added
- Light green scrollbar thumb.
- White, rounded Compose button with a light green hover.
- Sidebar: rounded light gray selected label, blue underlined selected text,
  Segoe UI / Open Sans labels at 14px, rounded light green hover.
- Message rows: soft blue unread, white read, pale yellow selected, light
  green hover.
- Density tweaks: 50px minimum row height, vertically centered rows,
  weight-500 sender/subject text, table layout fixes, small right padding,
  and two minor Gmail elements hidden (`.Zt`, `.bAw`).
- Section headers and comments throughout; selectors and values unchanged
  from the original uploaded stylesheet.

[Unreleased]: https://github.com/ckozlov-ASR/GMail-Swatches/compare/v3.0.0...HEAD
[3.0.0]: https://github.com/ckozlov-ASR/GMail-Swatches/compare/v2.3.0...v3.0.0
[2.3.0]: https://github.com/ckozlov-ASR/GMail-Swatches/compare/v2.2.0...v2.3.0
[2.2.0]: https://github.com/ckozlov-ASR/GMail-Swatches/compare/v2.1.0...v2.2.0
[2.1.0]: https://github.com/ckozlov-ASR/GMail-Swatches/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/ckozlov-ASR/GMail-Swatches/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/ckozlov-ASR/GMail-Swatches/releases/tag/v1.0.0
