# Changelog

All notable changes to this theme are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and versions follow
[Semantic Versioning](https://semver.org/).

## [Unreleased]

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

[Unreleased]: https://github.com/ckozlov-ASR/GMail_CSS/compare/v2.1.0...HEAD
[2.1.0]: https://github.com/ckozlov-ASR/GMail_CSS/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/ckozlov-ASR/GMail_CSS/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/ckozlov-ASR/GMail_CSS/releases/tag/v1.0.0
