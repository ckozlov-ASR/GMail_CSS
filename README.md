# Gmail CSS — Autumn Theme

A custom stylesheet that reskins the Gmail web interface with a warm autumn
palette (sage green, taupe, cream, golden amber), roomier message rows,
highlighted category tabs, and rounded "card" styling for messages in a
thread.

Current version: **2.1.0** — see [CHANGELOG.md](CHANGELOG.md).

## What it changes

| Area | Effect |
| --- | --- |
| Scrollbar | Sage green thumb (Chromium/WebKit browsers only) |
| Compose button | White pill with a faint border; turns sage on hover |
| Left sidebar | Taupe background on the selected label, blue underlined text, sage hover, sharper icons |
| Message list | Cream unread rows, off-white read rows, amber selected rows, sage hover |
| Category tabs | Amber background on the active Primary/Promotions/Updates tab, sage underline and hover |
| Thread view | Each message is a rounded card with an amber sender/date strip |
| Density | Taller rows (50px), slightly bolder sender/subject text, two minor UI elements hidden |

## Installing

Gmail has no built-in custom CSS setting, so the stylesheet is applied with a
user-style browser extension.

1. Install **Stylus** for your browser (Chrome Web Store, Edge Add-ons or
   Firefox Add-ons).
2. Open Gmail, click the Stylus icon and choose **Write style for:
   mail.google.com**.
3. Paste the contents of [`Gmail_autumn.css`](Gmail_autumn.css) and save.
4. Reload Gmail.

To update, replace the style's contents with the latest `Gmail_autumn.css`.

## Customizing

All colors, the corner radius, the sidebar font and the hover transition are
defined once as CSS custom properties in the `:root` block at the top of the
file. Edit those values to retune the whole theme.

### Different colors per Gmail account

[`Gmail_palette_ocean.css`](Gmail_palette_ocean.css) recolors the theme with
cool blues and seafoam for one account only. It overrides just the `:root`
colors, so install it as a second Stylus style next to `Gmail_autumn.css`
(both applying to `mail.google.com`):

1. Replace `your.account@example.com` in the file with that account's address.
2. Add it in Stylus as a new style for `mail.google.com`.

The style matches the address in the `aria-label` of Gmail's account avatar
button, so other accounts keep the Autumn colors. If each account has its
own Stylus (for example one browser profile per account), replace
the selector with `:root` and install the palette only in that profile. For
more accounts, copy the file and change the address and colors.

[`Gmail_palette_ember.css`](Gmail_palette_ember.css) works the same way with
copper, rust, peach and flame-orange colors, made to sit on a dark
chocolate-and-copper Gmail background. It starts with a Stylus
`==UserStyle==` header and an `@-moz-document` block, so paste the whole
file into a new style and it gets its own name ("Gmail Ember") instead of
clashing with an existing style.

Some variable names (`--gm-blue-unread`, `--gm-gray-selected`,
`--gm-yellow-selected`, `--gm-white-read`) date from the original green
theme and describe what each one styles, not its current color.

## Known limitations

- Gmail's class names (`.zE`, `.yO`, `.T-I-KE`, …) are auto-generated and
  undocumented. A Gmail update can rename them, and the matching rule then
  silently stops applying. The comments in the stylesheet say what each
  selector targets, to make them easier to re-find with the browser's
  developer tools.
- `.Zt` and `.bAw` are hidden but their exact purpose isn't documented. If
  something you expect is missing, comment that rule out first.
- Per-account palettes rely on Gmail's avatar `aria-label` including the
  email address. The Autumn colors can flash briefly while Gmail loads, and
  the account falls back to Autumn if Google rewords that label.
- The scrollbar color uses `::-webkit-scrollbar-thumb`, which Firefox ignores.

## Development notes

The theme has been developed iteratively with AI assistance (Claude).

- **April 2026 — v1.0.0.** The original green theme was uploaded as
  `Gmail_copy.css` alongside an experimental `Gmail2026_org.css`. The
  experiment was dropped and the main file renamed to `Gmail1_green.css`,
  then reformatted with section headers and comments without changing any
  selectors or values.
- **v2.0.0 rework.** The green file was cleaned up and restyled: the
  palette was rebuilt around an autumn desktop background and
  moved into CSS variables, duplicate rules were merged, a sidebar icon-fade
  bug was traced to Gmail's own translucent overlay, and two new sections
  (category tabs and thread cards) were added. Tab selectors were chosen to
  match the specificity of Gmail's own `background: none !important` rule so
  the override wins.

### Making changes

1. Edit `Gmail_autumn.css`, test it live by pasting into Stylus.
2. Add an entry under **Unreleased** in [CHANGELOG.md](CHANGELOG.md).
3. When releasing, move those entries under a new version heading, bump the
   version in this README, tag the commit (`git tag vX.Y.Z`) and publish a
   GitHub Release from the tag.

Versions follow [Semantic Versioning](https://semver.org/): a new major
version for a palette or layout overhaul, minor for new styled areas, patch
for selector fixes after Gmail updates.
