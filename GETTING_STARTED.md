# Narleaf Getting Started

For the full explanation of the concepts and design decisions, see `README.md` — this document only covers "how to write it."

## Introduction

Narleaf is a SCSS system that provides layout needs like container, grid, span, gap, and offset through ready-made utility classes. All classes come with the `nar-` prefix and can be customized by changing `$namespace`.

Throughout this document, the default configuration is used: a 12-column grid, with `sm` (640px), `md` (768px), `lg` (1024px), `xl` (1280px) breakpoints.

Every example can be copied and used as-is.

## Installation

Narleaf requires Dart Sass (it uses the `sass:map`, `sass:string`, `sass:math`, `sass:meta`, `sass:list` modules).

```scss
@use "narleaf" with (
  $namespace: "nar"
);
```

If you want to use the compiled CSS directly, just include the `.css` output in your project; in that case no build step is needed. The repository provides two ready-made variants (core classes only / all utilities); see the "Compiled CSS Variants" section in `README.md` to see which one suits you.

## First Container

`nar-container` centers content and applies a max width.

```html
<div class="nar-container">
  <p>Content goes here.</p>
</div>
```

If you want a full-page-width wrapper, use `nar-container-full`; it has the same behavior, with no max-width limit.

```html
<div class="nar-container-full">
  <p>Edge-to-edge content.</p>
</div>
```

## First Grid

`nar-grid` creates a 12-column CSS Grid container.

```html
<div class="nar-grid">
  <div class="nar-span-6">Left half</div>
  <div class="nar-span-6">Right half</div>
</div>
```

`nar-span-*` classes only work on a direct child of a `nar-grid`.

## Span Utilities

Determines how many columns an element spans (`1` to `12`).

```html
<div class="nar-grid">
  <div class="nar-span-4">4 columns</div>
  <div class="nar-span-4">4 columns</div>
  <div class="nar-span-4">4 columns</div>
</div>
```

To reset an element's span, use `nar-span-auto` (`grid-column: auto`).

## Responsive Span

Pattern: `nar-span-{breakpoint}-{value}`.

```html
<div class="nar-grid">
  <div class="nar-span-12 nar-span-md-6 nar-span-lg-4">
    Full width on mobile, half on md, one-third on lg.
  </div>
</div>
```

Classes work mobile-first: the `md` class takes effect at the `md` breakpoint (768px) and above.

## Gap Utilities

`nar-gap-*` sets both the row and column gap of the grid together.

```html
<div class="nar-grid nar-gap-24">
  <div class="nar-span-6">A</div>
  <div class="nar-span-6">B</div>
</div>
```

Available steps: `0, 8, 16, 24, 32, 40, 48`.

For gap between columns only, or between rows only, use `nar-gi-*` (gap-inline) and `nar-gb-*` (gap-block) — they share the same step values (`0, 8, 16, 24, 32, 40, 48`):

```html
<div class="nar-grid nar-gi-16 nar-gb-32">
  <div class="nar-span-6">A</div>
  <div class="nar-span-6">B</div>
</div>
```

## Gap Auto

`nar-gap-auto` applies a gap that automatically scales by breakpoint, instead of a fixed value.

```html
<div class="nar-grid nar-gap-auto">
  <div class="nar-span-6">A</div>
  <div class="nar-span-6">B</div>
</div>
```

With the default configuration: `base/sm: 16px`, `md/lg/xl: 24px`.

## Container Padding Utilities

`nar-pi-*` sets the container's horizontal padding (`padding-inline`) to a fixed scale step. Only works on the same element together with `nar-container` or `nar-container-full`.

```html
<div class="nar-container nar-pi-24">
  <p>24px horizontal padding.</p>
</div>
```

Available steps: `0, 16, 24, 32, 40`. Responsive variant: `nar-pi-{breakpoint}-{value}`.

## pi-auto

`nar-pi-auto` automatically adjusts the container's padding per breakpoint.

```html
<div class="nar-container nar-pi-auto">
  <p>Automatic padding based on screen size.</p>
</div>
```

With the default configuration: `base: 16px`, `sm/md: 24px`, `lg: 32px`, `xl: 40px`.

## Offset

`nar-offset-*` pushes an element to the right by the specified number of columns (`1` to `11`).

```html
<div class="nar-grid">
  <div class="nar-span-8 nar-offset-2">Centered 8-column block</div>
</div>
```

Responsive variant: `nar-offset-{breakpoint}-{value}`.

To cancel an offset applied at a smaller breakpoint, use `nar-offset-{breakpoint}-auto` — it resets the element back to normal auto-placement (`grid-column-start: auto`).

```html
<div class="nar-grid">
  <div class="nar-span-8 nar-offset-2 nar-offset-lg-auto">
    Offset by 2 columns until lg, no offset from lg onward.
  </div>
</div>
```

## col-start / col-end

Directly sets an element's starting and ending column line (`1` to `13`).

```html
<div class="nar-grid">
  <div class="nar-col-start-3 nar-col-end-9">From line 3 to line 9</div>
</div>
```

Responsive variants: `nar-col-start-{breakpoint}-{value}`, `nar-col-end-{breakpoint}-{value}`.

## Full Responsive Layout Example

An example combining container, automatic padding, grid, automatic gap, and responsive span together:

```html
<div class="nar-container nar-pi-auto">
  <div class="nar-grid nar-gap-auto">
    <div class="nar-span-12 nar-span-md-6 nar-span-lg-4">
      <!-- Card 1 -->
    </div>
    <div class="nar-span-12 nar-span-md-6 nar-span-lg-4">
      <!-- Card 2 -->
    </div>
    <div class="nar-span-12 nar-span-md-12 nar-span-lg-4">
      <!-- Card 3 -->
    </div>
  </div>
</div>
```

## Common Patterns

**Sidebar + content (3/9 ratio):**

```html
<div class="nar-grid nar-gap-lg-40">
  <aside class="nar-span-12 nar-span-lg-3">Sidebar</aside>
  <main class="nar-span-12 nar-span-lg-9">Content</main>
</div>
```

**Three-card row, single column on mobile:**

```html
<div class="nar-grid nar-gap-24">
  <div class="nar-span-12 nar-span-sm-6 nar-span-lg-4">Card 1</div>
  <div class="nar-span-12 nar-span-sm-6 nar-span-lg-4">Card 2</div>
  <div class="nar-span-12 nar-span-sm-6 nar-span-lg-4">Card 3</div>
</div>
```

**Centered narrow text block (using col-start):**

```html
<div class="nar-grid">
  <div class="nar-span-12 nar-span-md-8 nar-col-start-md-3">
    A narrow reading column, centered on wide screens.
  </div>
</div>
```

**Temporarily overriding auto at a specific breakpoint:**

```html
<div class="nar-container nar-pi-auto nar-pi-lg-40">
  <p>Automatic up to lg, fixed at 40px from lg onward.</p>
</div>
```

## Next Steps

This document only shows how to use the classes. See `README.md` for:

- Changing the grid column count, breakpoints, and namespace
- How to customize `pi-auto` / `gap-auto` values
- Which utility groups can be disabled at build time (`$nar-output-*` flags)
- The difference between the ready-made Minimal / Full compiled CSS files
- Compile-time validation rules
- Class compatibility and `:where()` specificity behavior
