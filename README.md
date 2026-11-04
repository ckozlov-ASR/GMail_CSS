# Gmail Swatches

Styles that reskin Gmail in the browser: roomier two-line inbox rows,
highlighted category tabs, rounded message cards in conversations, and a
choice of color themes (the swatches), one per Gmail account if you like.

Current version: **3.1.1** — see [CHANGELOG.md](CHANGELOG.md).

## How it's organized

| File | What it does |
| --- | --- |
| [`Base_GSwatch.css`](Base_GSwatch.css) | Layout and shapes for every account. Sets no palette; reads its colors from a theme. |
| [`themes/th_autumn.css`](themes/th_autumn.css) | Sage, taupe, cream and golden amber, for **one account** matched by email address. |
| [`themes/th_ocean.css`](themes/th_ocean.css) | Sky blue, slate, pale aqua and seafoam, for **one account** matched by email address. |
| [`themes/th_ember.css`](themes/th_ember.css) | Copper, rust, peach and flame orange, for **one account** matched by email address. |

Install the base once, plus one theme per account. Accounts without a
theme get the base's neutral grays.

## What the base changes

| Area | Effect |
| --- | --- |
| Scrollbar | Theme color (Chrome and Edge only) |
| Compose button | Theme color on hover; otherwise Gmail's own |
| Sidebar | Theme color and underlined text on the selected folder, hover color, clearer folder icons |
| Inbox rows | Separate unread, read, selected and hover colors |
| Category tabs | Accent color on the active Primary/Promotions/Updates tab, themed underline and hover |
| Conversations | Each message is a rounded card with a pale tinted sender/date strip |
| Text and spacing | Taller two-line inbox rows (subject above preview), bolder sender and subject text |

## Installing

Gmail has no built-in custom CSS setting, so the styles are applied with the
**Stylus** browser extension (Chrome Web Store, Edge Add-ons or Firefox
Add-ons). Each file becomes its own Stylus style:

1. In Stylus, choose **Manage → Write new style**.
2. Select everything in the editor and paste the whole file over it,
   including the `==UserStyle==` header at the top, then save. Without that
   header Stylus reports "Could not find metadata".
3. Repeat for each file:
   - `Base_GSwatch.css` (always)
   - one file from `themes/` per account, after replacing
     `your.account@example.com` with that account's address
4. Reload Gmail.

The styles only apply on mail.google.com, and their order in Stylus doesn't
matter.

To update, paste the latest version of a file over its style. Re-enter your
email address in each theme when you do.

## Customizing

You can change colors, sizes and rounding without knowing CSS. Every
setting in the files has a plain-English note above it saying what it
changes and a suggested range, for example:

```css
/* Thread header: pale amber. Strip behind the sender and date at
   the top of each message in a conversation.
   Strength: 0.10 lighter … 0.18 now … 0.30 darker */
--gm-thread-header: rgba(230, 180, 90, 0.18);
```

Edit the value in your Stylus style, keeping the punctuation as it is, and
save; Gmail updates immediately. In `rgba(R, G, B, S)` colors, the last
number is the strength, from 0 (invisible) to 1 (solid). To choose a new
color, search the web for "color picker" and copy its RGB numbers or
`#` code.

### Theme colors

Each theme sets the same eight variables, named for what they color:

| Variable | Used for |
| --- | --- |
| `--gm-hover-soft` | Scrollbar thumb, Compose hover |
| `--gm-hover` | Row, sidebar label and tab hover |
| `--gm-label-selected` | Selected sidebar label background |
| `--gm-label-text` | Selected sidebar label text |
| `--gm-row-unread` | Unread message rows |
| `--gm-row-read` | Read message rows, thread cards |
| `--gm-accent` | Selected rows, active tab, thread header underline |
| `--gm-thread-header` | Thread sender/date strip (a pale tint of the accent) |

### A new theme or another account

Copy `themes/th_ocean.css`, give it a new `@name`, change the email address
and the eight colors, and add it to Stylus as another style.

### How account matching works

Each theme applies only when Gmail's account button (top right) mentions
its email address, using `html:has(a[aria-label*="you@example.com"])`.
This works whether your browser shares one Stylus across accounts or gives
each profile its own.

To make a theme the default for every account without its own, change its
selector to `:root`. Email-matched themes still win on their accounts.

### Shapes and spacing

These settings are in the **Settings you can change** block at the top of
`Base_GSwatch.css` and apply to every theme:

| Variable | What it changes | Range |
| --- | --- | --- |
| `--gm-radius` | Rounding of tabs and message cards | 0px square … 14px … 24px very round |
| `--gm-label-radius` | Rounding of the selected/hovered sidebar folder's right end | 0px … 16px … 20px full pill |
| `--gm-row-height` | Height of each inbox row | 40px compact … 50px … 64px roomy |
| `--gm-label-font-size` | Sidebar folder name size | 13px … 14px … 16px |
| `--gm-font-stack` | Sidebar folder name font | Any installed fonts, `sans-serif` last |
| `--gm-transition` | How fast hover colors fade in | 0s instant … 0.15s … 0.4s slow |

To hide Gmail's right-hand side panel (Calendar, Keep, Tasks), change the
`.Zt` rule at the end of the base to `.Zt, .bAw`.

## Known limitations

- Gmail's class names (`.zE`, `.yO`, `.T-I-KE`, …) are auto-generated. A
  Gmail update can rename them, and the matching rule quietly stops
  working. The comments in the base say what each rule targets, to help
  find the new name with the browser's developer tools.
- Account themes depend on Gmail's account button mentioning the email
  address. Neutral grays can flash briefly while Gmail loads.
- Firefox ignores the scrollbar color.

## Development notes

Developed with AI assistance (Claude).

- **v1.0.0 (April 2026).** The original green theme, reformatted with
  section headers and comments.
- **v2.0.0.** Restyled around an autumn palette held in CSS variables, with
  new category-tab and conversation-card sections and a fix for faded
  sidebar icons.
- **v2.1–2.3.** Ocean and Ember added as per-account themes matched by
  email address, and `==UserStyle==` headers so Stylus accepts the files.
- **v3.0.0.** Layout moved to its own base file, each palette became a
  short theme file, and the color variables were named by role.
- **v3.1.** Plain-English notes and ranges on every setting, a softer
  conversation header and spacing fixes.

### Making changes

1. Edit `Base_GSwatch.css` (layout) or a file in `themes/` (colors), and test
   it live by pasting into Stylus.
2. Add an entry under **Unreleased** in [CHANGELOG.md](CHANGELOG.md).
3. When releasing, move those entries under a new version heading, bump the
   version in this README and in each file's `@version` line, tag the commit
   (`git tag vX.Y.Z`) and publish a GitHub Release from the tag.

Versions follow [Semantic Versioning](https://semver.org/): a new major
version for a palette or layout overhaul, minor for new styled areas, patch
for selector fixes after Gmail updates.
