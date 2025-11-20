# ThimbleCSS

**ThimbleCSS** is a lightweight, modern SCSS micro-framework.  
It provides a minimal baseline for typography, layout, utilities, and design tokens—without imposing a full design system or component library.

Thimble is intended to be **imported into your own SCSS pipeline**, not consumed as a precompiled CSS file.

---

## Features

- Modular SCSS architecture  
- Configurable variables, breakpoints, and color system  
- Utility classes for grids, spacing, media, and typography  
- Small surface area, easy to override  
- No runtime dependencies

---

## Installation

```bash
npm install thimblecss
```

## Usage

``` SCSS
@use "thimblecss" as *;

// OR customize variables and modules before import:

@use "thimblecss" with (
  $small-break: 600px,
  $medium-break: 900px,
  $large-break: 1200px,
  $xlarge-break: 1400px
);
```

## Documentation
Full documentation, examples, and guidance are available at: [ThimbleCSS](https://thimblecss.com/)
