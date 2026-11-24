# ThimbleCSS

**ThimbleCSS** is a lightweight, modern CSS micro-framework, about 6KB gzipped.
It gives you the parts that rarely change between projects (normalized defaults, a fluid type scale, layout, and utilities) and keeps them easy to override. There's no component library and no look to fight.

ThimbleCSS is **plain CSS**: no preprocessor and no build step. Link it from a CDN, install it from npm, or download it.

---

## Features

- **No look to accept.** Every token is a CSS variable you can override.
- **Your CSS always wins.** ThimbleCSS lives in cascade layers, so a plain selector overrides it. `!important` is used only where it protects users (reduced motion, reduced transparency, and the `hidden` attribute).
- **Change one color, the rest follows.** Hover and active colors are mixed from the base color with `color-mix()`.
- **Accessible by default.** Reduced motion, visible focus rings, and form errors that wait until the user has interacted.
- Normalized browser defaults
- A fluid type scale
- CSS Grid and flexbox layouts, responsive at four breakpoints
- Utility classes for spacing, media, and typography
- Light and dark mode, built in
- No runtime dependencies

---

## Installation

### CDN

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/thimblecss@4/dist/thimble.min.css">
```

### npm

```bash
npm install thimblecss
```

```css
@import "thimblecss";
```

### Download

Grab `dist/thimble.css` or `dist/thimble.min.css` from this repo and link it like any other stylesheet. The modular source files are in `css/`.

---

## Usage

### Customizing

Every token is a CSS custom property in [`css/tokens.css`](css/tokens.css). Copy the ones you want to change into your own `:root`. There's no need to copy the whole file:

```css
:root {
  --blue: #0a6e4f;
  --primary-font: "Inter", sans-serif;
  --gap: 1.5rem;
}
```

### Your CSS always wins

ThimbleCSS puts all of its styles in cascade layers. Styles outside a layer beat any layered style, whatever the specificity and whichever file loads first, so plain overrides just work:

```css
/* No !important, no extra specificity */
.button { border-radius: 0; }
h1 { font-weight: 900; }
```

The layers, from lowest to highest priority: `thimble.tokens`, `thimble.normalize`, `thimble.base`, `thimble.accessibility`, `thimble.layout`, `thimble.elements`, `thimble.utilities`.

### Light and dark mode

ThimbleCSS sets `color-scheme: light dark` and defines its colors with `light-dark()`, so it follows the visitor's system setting. Use the same function for your own colors, or pin the scheme:

```css
:root {
  --heading-color: light-dark(var(--jet), white);

  /* Or force a single scheme */
  color-scheme: light;
}
```

### Layout

```html
<!-- Stacks on phones, 3 columns from 768px up -->
<div class="grid medium-cols-3">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
</div>

<!-- 12-column grid: content and sidebar -->
<div class="grid medium-cols-12">
  <main class="medium-span-8">Content</main>
  <aside class="medium-span-4">Sidebar</aside>
</div>

<!-- As many columns as fit, each at least --grid-min (16rem) -->
<div class="grid auto">
  <div>Card</div>
  <div>Card</div>
  <div>Card</div>
</div>

<!-- Flexbox row -->
<div class="flex align-center justify-between">
  <span class="fill">Grows</span>
  <span class="fit">Fits</span>
</div>
```

A span is capped at the grid's current column count, so `.span-8` in a 3-column grid fills one row instead of breaking the layout.

### Accessibility

- Keyboard focus gets a visible ring through `:focus-visible`. Adjust it with `--focus-ring`, `--focus-ring-color`, and `--focus-ring-offset`.
- With `prefers-reduced-motion`, animations and transitions finish instantly. Add `.motion-ok` to keep essential motion, like a spinner.
- With `prefers-reduced-transparency`, backdrop filters are removed.
- `.sr-only` hides content visually but keeps it for screen readers, and shows it on focus, so it works for skip links.
- Invalid form fields use `:user-invalid`, so errors only show after someone has edited the field. Use `aria-invalid="true"` to flag a field from your own validation.

---

## Breakpoints

ThimbleCSS is mobile-first. Unprefixed classes apply at every width, and a prefixed class applies from its breakpoint up.

| Prefix     | Min width | Pixels |
|------------|-----------|--------|
| *(none)*   | 0         | 0      |
| `small-`   | 30em      | 480px  |
| `medium-`  | 48em      | 768px  |
| `large-`   | 64em      | 1024px |
| `xlarge-`  | 80em      | 1280px |

Prefixes work with `cols-`, `span-`, `order-`, `span-full`, `row`, `column`, `fit`, `fill`, `hide`, and the `text-` alignment classes. The `-show` classes work the other way round: `.medium-show` hides an element *below* 768px.

Media queries can't read custom properties, so the breakpoints are fixed. To change them, edit the media queries in `css/layout-responsive.css` and `css/utilities.css`.

---

## Browser Support

ThimbleCSS supports Chrome and Edge 123+, Safari 17.5+, and Firefox 128+.

`textarea.autogrow` uses `field-sizing: content`, which needs Chrome and Edge 123+, Safari 26.2+, or Firefox 152+. In older browsers the textarea keeps its normal size.

---

## Upgrading from v3

v4 drops Sass and replaces the flex `.grid` and `.cell` system with CSS Grid. See the [changelog](changelog.md) for the full list of changes and a migration guide. ThimbleCSS v3 (Sass) is still available on npm as `thimblecss@3`.

---

## Documentation

Full documentation and live examples are at [thimblecss.com](https://thimblecss.com/).
