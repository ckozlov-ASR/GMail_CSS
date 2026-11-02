# Gmail CSS — Base + Themes

Custom styles that reskin the Gmail web interface: roomier message rows,
highlighted category tabs, rounded "card" styling for messages in a thread,
and a choice of color themes, with a different theme per Gmail account if you
like.

Current version: **3.0.0** — see [CHANGELOG.md](CHANGELOG.md).

## How it's organized

| File | What it does |
| --- | --- |
| [`Gmail_base.css`](Gmail_base.css) | Layout and shapes for every account. Sets no palette; reads its colors from a theme. |
| [`themes/autumn.css`](themes/autumn.css) | Sage, taupe, cream and golden amber, for **one account** matched by email address. |
| [`themes/ocean.css`](themes/ocean.css) | Sky blue, slate, pale aqua and seafoam, for **one account** matched by email address. |
| [`themes/ember.css`](themes/ember.css) | Copper, rust, peach and flame orange, for **one account** matched by email address. |

Install the base once, plus one theme per account. Accounts without a
theme get the base's neutral grays.

## What the base changes

| Area | Effect |
| --- | --- |
| Scrollbar | Theme-colored thumb (Chromium/WebKit browsers only) |
| Compose button | White pill with a faint border; theme color on hover |
| Left sidebar | Theme color on the selected label with underlined text, hover color, sharper icons |
| Message list | Separate unread, read and selected row colors, hover color |
| Category tabs | Accent background on the active Primary/Promotions/Updates tab, themed underline and hover |
| Thread view | Each message is a rounded card with an accent sender/date strip |
| Density | Taller rows (50px), bolder sender and subject text, two minor UI elements hidden |

## Installing

Gmail has no built-in custom CSS setting, so the styles are applied with the
**Stylus** browser extension (Chrome Web Store, Edge Add-ons or Firefox
Add-ons). Each file becomes its own Stylus style:

1. In Stylus, choose **Manage → Write new style**.
2. Select everything in the editor and paste the whole file over it,
   including the `==UserStyle==` header at the top, then save. Without that
   header Stylus reports "Could not find metadata".
3. Repeat for each file:
   - `Gmail_base.css` (always)
   - one file from `themes/` per account, after replacing
     `your.account@example.com` with that account's address
4. Reload Gmail.

Every file wraps its rules in `@-moz-document domain("mail.google.com")`, so
the styles only apply to Gmail, and the order of styles in Stylus doesn't
matter.

To update, paste the latest version of a file over its style. Re-enter your
email address in Ocean or Ember when you do.

## Customizing

### Theme colors

Each theme sets the same seven variables, named for what they color:

| Variable | Used for |
| --- | --- |
| `--gm-hover-soft` | Scrollbar thumb, Compose hover |
| `--gm-hover` | Row, sidebar label and tab hover |
| `--gm-label-selected` | Selected sidebar label background |
| `--gm-label-text` | Selected sidebar label text |
| `--gm-row-unread` | Unread message rows |
| `--gm-row-read` | Read message rows, thread cards |
| `--gm-accent` | Selected rows, active tab, thread header strip |

The base gives each one a neutral gray fallback, so Gmail still looks
reasonable with the base alone.

### A new theme or another account

Copy `themes/ocean.css`, give it a new `@name`, change the email address and
the seven colors, and add it to Stylus as another style.

### How account matching works

Account themes match the address in the `aria-label` of Gmail's account
avatar button (top right), using
`html:has(a[aria-label*="you@example.com"])`. This works whether your
browser shares one Stylus across accounts or, like separate browser
profiles, gives each its own.

To give every unmatched account a default theme, change that theme's
selector to `:root`. The email-matched selector outranks `:root`, so the
other themes still win on their own accounts. With separate profiles you
can likewise use `:root` and install the theme only in that profile.

### Shapes and spacing

Corner radius, sidebar font, the Compose border and the hover transition
are variables in the `:root` block at the top of `Gmail_base.css`.

## Known limitations

- Gmail's class names (`.zE`, `.yO`, `.T-I-KE`, …) are auto-generated and
  undocumented. A Gmail update can rename them, and the matching rule then
  silently stops applying. The comments in the stylesheet say what each
  selector targets, to make them easier to re-find with the browser's
  developer tools.
- `.Zt` and `.bAw` are hidden but their exact purpose isn't documented. If
  something you expect is missing, comment that rule out first.
- Account themes rely on Gmail's avatar `aria-label` including the
  email address. The base's neutral grays can flash briefly while Gmail
  loads, and the account falls back to them if Google rewords that label.
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
- **v2.1–2.3.** Ocean and Ember were added as per-account overrides on top of
  the Autumn file, matched by email address so one shared Stylus can theme
  several accounts. Every file gained
  a `==UserStyle==` header after Stylus rejected pastes without one.
- **v3.0.0 split.** With three palettes, Autumn was both the layout and the
  default colors, and its variable names (`--gm-blue-unread` holding cream)
  no longer matched. The layout moved to `Gmail_base.css`, each palette
  became a short file in `themes/`, and the variables were renamed by role.

### Making changes

1. Edit `Gmail_base.css` (layout) or a file in `themes/` (colors), and test
   it live by pasting into Stylus.
2. Add an entry under **Unreleased** in [CHANGELOG.md](CHANGELOG.md).
3. When releasing, move those entries under a new version heading, bump the
   version in this README, tag the commit (`git tag vX.Y.Z`) and publish a
   GitHub Release from the tag.

Versions follow [Semantic Versioning](https://semver.org/): a new major
version for a palette or layout overhaul, minor for new styled areas, patch
for selector fixes after Gmail updates.
