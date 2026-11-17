# ThimbleCSS

**ThimbleCSS** is a lightweight, modern CSS micro-framework, ~5KB gzipped.  
It provides a minimal baseline for typography, layout, utilities, and design tokens—without imposing a full design system or component library.

Thimble is **plain CSS**: no preprocessor or build step required. Drop it in from a CDN, or install it from npm.

---

## Features

- Plain CSS with native nesting, custom properties, and cascade layers  
- Your own CSS always wins: no specificity fights, and `!important` only where it protects users (reduced motion, reduced transparency, the `hidden` attribute)  
- CSS Grid and flexbox layouts, responsive at four breakpoints  
- Fluid type scale
- Built-in light and dark mode  
- Utility classes for spacing, media, and typography  
- Small surface area, easy to override  
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

Grab `dist/thimble.css` or `dist/thimble.min.css` from this repo and link it like any stylesheet.

---

## Usage

### Customizing

Every setting is a CSS variable in [`css/settings.css`](css/settings.css). Copy the variables you want to change into your own `:root`. You don't need to copy the whole file:

```css
:root {
  --blue: #0a6e4f;
  --primary-font: "Inter", sans-serif;
  --gap: 1.5rem;
}
```

Thimble lives in cascade layers, so your unlayered CSS always overrides it, whichever file loads first.

### Picking modules

Only need some of Thimble? Import the files you want from `css/`, keeping the layer order line first:

```css
@layer thimble.settings, thimble.normalize, thimble.base, thimble.accessibility, thimble.layout, thimble.elements, thimble.utilities;

@import "thimblecss/css/settings.css";
@import "thimblecss/css/normalize.css";
@import "thimblecss/css/base.css";
@import "thimblecss/css/accessibility.css";
@import "thimblecss/css/layout.css";
@import "thimblecss/css/layout-responsive.css";
```

`settings.css` is always required. `buttons.css`, `forms.css`, and `utilities.css` are optional.

### Layout

```html
<!-- Stacks on small screens, 3 columns from medium up -->
<div class="grid medium-cols-3">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
</div>

<!-- 12-column grid -->
<div class="grid medium-cols-12">
  <main class="medium-span-8">Content</main>
  <aside class="medium-span-4">Sidebar</aside>
</div>

<!-- Flexbox row -->
<div class="flex align-center justify-between">
  <span class="fill">Grows</span>
  <span class="fit">Fits</span>
</div>
```

---

## Breakpoints

Thimble is mobile-first. Unprefixed classes apply at every size; prefixed classes apply from that breakpoint up.

| Prefix     | Min width | Pixels |
|------------|-----------|--------|
| *(none)*   | 0         | 0      |
| `small-`   | 30em      | 480px  |
| `medium-`  | 48em      | 768px  |
| `large-`   | 64em      | 1024px |
| `xlarge-`  | 80em      | 1280px |

Prefixes work with `cols-`, `span-`, `order-`, `row`, `column`, `fit`, `fill`, `hide`, and `text-` alignment classes. `.medium-show` and the other `-show` classes hide an element *below* that breakpoint.

To change breakpoints, edit the media queries in `css/layout-responsive.css` and `css/utilities.css`.

---

## Browser Support

Thimble targets current evergreen browsers: Chrome/Edge 123+, Safari 17.5+, and Firefox 128+.

---

## Upgrading from v3

v4 drops Sass and replaces the flex `.grid` and `.cell` system with CSS Grid. See the [changelog](changelog.md) for the full list of changes and a migration guide. Thimble v3 (SCSS) remains available on npm as `thimblecss@3`.

---

## Documentation
Full documentation, examples, and guidance are available at: [ThimbleCSS](https://thimblecss.com/)
