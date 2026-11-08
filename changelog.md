Change Log
==============

## v4.0.0

This is a major rewrite, the fourth since Thimble's inception. We started with floats, moved to flex, then Sass, and now we're back to plain CSS because preprocessors are no longer needed. This release has breaking changes for projects on any earlier version; see **Migrating from v3** below.

### Structure
- converted from SCSS to plain CSS with native nesting and custom properties
- organized into cascade layers: settings, normalize, base, accessibility, layout, components, utilities. Your own unlayered CSS always wins, with no specificity fights
- utilities no longer use `!important`; layer order does the work
- optional modules are chosen by editing the imports in `thimble.css` (replaces the `$include-*` options)
- breakpoints are fixed at 30, 48, 64 and 80em (480, 768, 1024 and 1280px). Sass-configured breakpoints are gone; edit the media queries in `layout-responsive.css` and `utilities.css` to change them
- the npm package now includes a bundled `dist/thimble.css` and a minified `dist/thimble.min.css`

### Normalize and accessibility
- replaced sanitize with a smaller normalize
- removed `:focus { outline: 0 }`; keyboard focus is now visible and styled with `--focus-ring`
- images, video and canvas are now `display: block`
- reduced motion and reduced transparency live in their own accessibility layer; add `.motion-ok` to opt an element and its children out of reduced motion
- added `.sr-only`, which becomes visible when focused so it works for skip links

### Typography
- fluid type scale (`--type-neg-1` to `--type-5`) replaces the fixed rem sizes
- tighter heading line-height, bold headings, and h5 and h6 styled apart from the rest
- `text-wrap: balance` on headings and `pretty` on body text
- headings get more space above than below
- `.hero` is now a standalone class
- links transition color only and use a derived hover color
- added `--mono-font` for `code`, `kbd`, `samp` and `pre`, and a default `hr` style
- removed the `.vw` heading classes and the `.sup` and `.sub` classes

### Layout
- `.grid` is now CSS Grid: `.cols-N`, `.span-N`, `.span-full`, `.order-N`, and `.grid.auto` for intrinsic columns (sized by `--grid-min`)
- spans are capped at the grid's current column count, so `.span-6` can no longer overflow a one-column grid on small screens. Spans other than `.span-full` are ignored inside `.grid.auto`
- `.flex` is flexbox with a gap: `.wrap`, `.row`, `.column`, `.row-reverse`, `.column-reverse`, `.fit` and `.fill`. Flex rows no longer wrap by default
- `.cols-`, `.span-`, `.order-`, `.row`, `.column`, `.fit` and `.fill` have `small-`, `medium-`, `large-` and `xlarge-` versions
- gutters are `gap`, set with `--gap`
- alignment classes are `.align-*`, `.justify-*` and `.self-*`; `.align-*` no longer sets `align-self`
- `.align-wide` and `.align-full` are renamed `.break-wide` and `.break-full`
- added `.container-tiny`; container widths are now in rem
- removed `.cell`, `.edge`, `.half-edge`, `.collapse`, `.collapse-padding`, `.fifth`, the word sizes (`.one` to `.twelve`), `.vertical`, `.reverse`, `.nowrap` and `.wrap-reverse`

### Buttons and forms
- hover and active colors are computed at runtime with `color-mix()`, so the color tints are no longer needed
- buttons: added a disabled state and `.plain` for unstyled buttons. `:focus-visible` replaces `:focus`, and the primary hover no longer turns gray
- forms: styles apply only to text-like fields, select and textarea; plain labels are blocks, and checkbox and radio labels use flex
- added `:user-invalid` and `aria-invalid` styling, placeholder color, and `textarea.autogrow`
- checked radios stay visible in Windows High Contrast mode
- submit buttons are no longer full width; add `.full`

### Utilities
- removed `.flex` from utilities (it is now a layout class and adds a gap)
- `.full` now works on any element, not just media
- `.rounded-full` uses 9999px, so non-square elements become pills instead of ovals
- `.clear` is now `display: flow-root`
- added `.text-muted`
- added spacing: gap, padding, margin-top, margin-bottom and `.mx-auto`, on a `--space-1` to `--space-8` scale
- per-breakpoint hide, show and text-align classes are kept

### Tokens and colors
- removed the `-l1`, `-l2`, `-d1` and `-d2` color tints and the `--mix-*` values
- links, the focus ring and buttons use lighter blues in dark mode for contrast
- added shadow, spacing, radius, leading and `--mono-font` tokens
- renamed `--header-color` to `--heading-color`
- removed `--subfont-color` (use `--muted-color`), `--cell-margin` and `--cell-padding`
- replaced `--easing` and the `--*-speed` tokens with `--duration` and `--ease`
- removed `--form-hover-border`, `--form-disabled-background`, `--form-disabled-border`, `--button-hover-background`, `--button-active-background` and the secondary hover and active tokens; these colors are now derived. Use `--button-hover-mix` and `--button-active-mix` to tune them
- removed the Sass mixins (`scrollbar`, `columns`, `quick-center`)

### Migrating from v3
- `.grid` with `.cell.six` becomes `.grid.cols-12` with `.span-6`. To stack on small screens, use `.grid.medium-cols-12` with `.medium-span-6`
- `.cell.fill` and `.cell.fit` in a row become `.flex` with `.fill` and `.fit`; add `.wrap` if the row should wrap
- `.vertical` becomes `.flex.column`
- the old `.flex` utility now adds a gap; add `.gap-0` where you need the old behavior
- `.justify-space` becomes `.justify-between`, `.align-top` becomes `.align-start`, and `.align-bottom` becomes `.align-end`
- `.align-wide` and `.align-full` become `.break-wide` and `.break-full`
- remove `.edge`, `.half-edge` and `.collapse`; use `.gap-0` for no gap
- `h1.hero` becomes `.hero`
- images inside text are now blocks; add `.inline-block` where an image should sit in a line of text
- rename `--header-color` to `--heading-color` and any `--subfont-color` to `--muted-color`
- replace the Sass breakpoint options with edits to `layout-responsive.css` and `utilities.css`


## v3.0.1
- rename .super-heading to .hero
- add .full class to images to prevent auto fill
- fix duplicate button code in forms include

## v3.0.0
This is a major new releast and reworking of thimble for a modern approach to variables.

- moved all overrides to CSS variables
- added optional buttons module
- added optional utilities module
- added optional forms module
- moved breakpoints to config file
- updated colors
- added color helper for light/dark variation
- added built in light/dark mode
- added new container classes
- fixed incorrectly named header classes
- removed outdated video container and added ratio helper classes

## V2.3.0
- remove legacy precompiled css file

## V2.2.6
- add edge and half-edge classes to grid
- rework visibility utility to remove display inherit
- add sizing-down mixin

## V2.2.5
- add xlarge container size

## V2.2.4
- add responsive fit and fill classes
- add back in min-height and min-width to cell base class

## V2.2.3
- Add responsive heading sizes

## V2.2.2
- Add $line-height variable to overrides
- Use $line-height to apply margin-bottom to headers in rem

## V2.2.1
- Update Sanitize. Based on https://github.com/csstools/sanitize.css/
- Remove legacy webkit and moz prefixes
- Remove transform mixin
- Remove keyframe mixin
- Remove trailing semi-colons from core
- Remove header class sizing
- Remove super-header for all but h1
- Add reduced motion query to core
- Add text underline class
- Add !default to sass overrides
- Add orange and violet colors
- Update large media break to 1280px

## V2.14
- Fix mixins typo for large-down media query

## V2.13
- Rename full, small-full, large-full to container, small-container, large-container respectively
- Add align-full
- Add align-wide
- Update Readme

## V2.12
- Add h6 sizing in augmented fourth headers
- Add collapse-padding option to grid
- Fix super-header sizing

## V2.11
- Add large site width option

## V2.1
- Fix xlarge hide class
- Update typography system to augmented fourth scale
- remove class requirement for headers

## v2.0
- Remove cards
- Remove buttons
- Remove box styles
- Remove Style Guide
- Removed .css version
- Rebuild grid - Renamed Rows and columns to reflect a single grid box, removed padding from grid cells and replaced with margins for better background handling
- create mixin for grid and typographic breakpoint sizing
- create mobile first media mixins 

## v1.1-beta
- add style-guide html and css
- move scss to own file
- pull out mixins
- add .em class for italics

## v1.0.4-beta
- remove modernizr tags
- fix small validation errors in .css file
- move css into own folder

## v1.0.3.5-beta
- Fix multiline css media query

## v1.0.3-beta
- Add variable for header font
- Clean up white-space
- Remove some old vendor prefixes
- Remove ordinal flex prefix
- Remove old flexbox standards

## v1.0.2-beta
- Add class 'inside' to rows to allow align properly inside other Rows
- fix row's min-width
- fix cell's max-width
- add medium only media queries anc cell widths

## v1.0.1-beta  
### Fixed bugs
- Fix column row's spacing with .cell.fit

### Implemented enhancements
- Add Changelog!
