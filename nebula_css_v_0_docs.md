# NebulaCSS v0.1 — Documentation

A tiny, highly‑customizable CSS framework built on **design tokens**, **cascade layers**, and **zero‑build theming**. Ships with polished **components**, **utilities**, **responsive variants**, and **container-query helpers**.

> **Version:** 0.1 · **License:** MIT · **Author:** ChatGPT

---

## Table of Contents
- [Getting Started](#getting-started)
- [Core Concepts](#core-concepts)
- [Design Tokens](#design-tokens)
  - [Color System](#color-system)
  - [Typography](#typography)
  - [Spacing](#spacing)
  - [Radii](#radii)
  - [Shadows](#shadows)
  - [Layout & Breakpoints](#layout--breakpoints)
  - [Motion](#motion)
  - [Themes & Palettes](#themes--palettes)
  - [Density Presets](#density-presets)
- [Base Styles](#base-styles)
- [Components](#components)
  - [Buttons](#buttons)
  - [Badges / Chips](#badges--chips)
  - [Cards](#cards)
  - [Forms](#forms)
  - [Switch](#switch)
  - [Navbar](#navbar)
  - [Tabs](#tabs)
  - [Alerts](#alerts)
  - [Modal (Dialog)](#modal-dialog)
  - [Tooltip](#tooltip)
  - [Glassmorphism Helper](#glassmorphism-helper)
- [Utilities](#utilities)
  - [Display](#display)
  - [Flexbox](#flexbox)
  - [Grid](#grid)
  - [Spacing Utilities](#spacing-utilities)
  - [Sizing](#sizing)
  - [Borders & Radii](#borders--radii)
  - [Background / Text / Rings](#background--text--rings)
  - [Typography Utilities](#typography-utilities)
  - [Position](#position)
  - [Shadows Utilities](#shadows-utilities)
  - [Transitions](#transitions)
  - [Animations](#animations)
  - [Utility Wrappers](#utility-wrappers)
- [Responsive Variants](#responsive-variants)
- [Container Queries](#container-queries)
- [Color Helper Classes](#color-helper-classes)
- [Print & Reduced Motion](#print--reduced-motion)
- [Theming & Overrides via Cascade Layers](#theming--overrides-via-cascade-layers)
- [Examples](#examples)
- [Roadmap](#roadmap)
- [Appendix: Quick Class Index](#appendix-quick-class-index)

---

## Getting Started

**Include the stylesheet** (either link to `nebula.css` or paste the CSS into a `<style>` block):
```html
<link rel="stylesheet" href="nebula.css">
```

**Drop in a component**:
```html
<button class="btn is-primary">Get Started</button>
```

**Pick a theme**:
```html
<body data-theme="dark">
  <!-- or -->
  <div class="theme-ocean"> ... </div>
</body>
```

---

## Core Concepts

NebulaCSS is organized with **cascade layers** for safe overrides:

```
@layer tokens, base, components, utilities;
```

- **tokens** — global design variables (colors, type scale, spacing, etc.)
- **base** — reset and sensible defaults (typography, container, focus)
- **components** — buttons, cards, forms, etc.
- **utilities** — small, atomic-ish helpers for layout and design

> Override tokens or components in your own CSS **after** NebulaCSS loads, using the same layer names to keep specificity in check.

---

## Design Tokens

Tokens live under `@layer tokens`. Override them anywhere in your app—globally on `:root`, or locally via a wrapper element.

### Color System

**Semantic hues** (HSL):
- `--primary-h/s/l`, `--secondary-h/s/l`, `--accent-h/s/l`
- `--success-h/s/l`, `--warning-h/s/l`, `--danger-h/s/l`
- `--surface-h/s/l` (base surfaces), `--surface-contrast-h/s/l` (text on surface)

**Derived tokens** (already computed for you):
- `--primary`, `--primary-600`, `--primary-700`
- `--secondary`, `--accent`
- `--success`, `--warning`, `--danger`
- Surfaces: `--surface`, `--surface-1/2/3`
- Text/Border: `--text`, `--text-muted`, `--border`, `--border-strong`

**Dark Mode** (opt-in):
```html
<body data-theme="dark"> ... </body>
```
Dark mode swaps surface and contrast tokens, text, and border values.

### Typography
- **Font families**: `--font-sans`, `--font-mono`
- **Fluid type scale** using CSS `clamp()`:
  - `--step--2`, `--step--1`, `--step-0`, `--step-1`, `--step-2`, `--step-3`, `--step-4`, `--step-5`
- Headings map to these steps in `@layer base`.

### Spacing
- **Global density**: `--scale` (default `1`)
- Spacing tokens: `--space-0` to `--space-8`

### Radii
- `--radius-xs`, `--radius-sm`, `--radius`, `--radius-md`, `--radius-lg`, `--radius-xl`, `--radius-2xl`, `--radius-full`

### Shadows
- `--shadow-sm`, `--shadow`, `--shadow-lg`, `--shadow-xl`

### Layout & Breakpoints
- `--container`: max inline size for `.container`
- `--content`: measure for `.prose`
- Breakpoints: `--bp-sm (40rem)`, `--bp-md (48rem)`, `--bp-lg (64rem)`, `--bp-xl (80rem)`

### Motion
- Easing: `--easing`
- Durations: `--speed-fast`, `--speed`, `--speed-slow`

### Themes & Palettes

**Built-in palettes** (override hues at any wrapper):
```html
<div class="theme-ocean"> ... </div>
<div class="theme-rose"> ... </div>
<div class="theme-amber"> ... </div>
```

**Custom palette**:
```css
@layer tokens {
  :root {
    --primary-h: 265; --primary-s: 90%; --primary-l: 56%;
    --accent-h: 295;  --accent-s: 85%; --accent-l: 62%;
  }
}
```

### Density Presets
- `.density-compact` → `--scale: .9`
- `.density-comfort` → `--scale: 1`
- `.density-cozy` → `--scale: 1.1`

Wrap any subtree with a density class to scale paddings, gaps, etc.

---

## Base Styles

- Modern reset, border-box sizing, fluid headings
- Media elements are block-level and responsive by default
- **Focus rings** use `:focus-visible` with theme color
- **A11y helper**: `.sr-only` for visually hidden text
- **Layout helpers**: `.container` (centered, max width), `.prose` (readable measure)

Example:
```html
<main class="container prose">
  <h1>Welcome</h1>
  <p>Body copy with sensible defaults.</p>
</main>
```

---

## Components

### Buttons
**Base class:** `.btn`

**Variants:**
- `.is-primary`, `.is-secondary`, `.is-accent`, `.is-danger`, `.is-success`
- `.is-outline`, `.is-ghost`

**Sizes:** `.is-sm`, `.is-lg`, and `.btn-icon` (square, circular)

**Example:**
```html
<button class="btn">Default</button>
<button class="btn is-primary">Primary</button>
<button class="btn is-outline">Outline</button>
<button class="btn is-ghost">Ghost</button>
<button class="btn is-danger is-lg">Delete</button>
<button class="btn btn-icon is-primary" aria-label="Settings">⚙️</button>
```

**Notes:** Hover raises elevation; focus ring on `:focus-visible`.

---

### Badges / Chips
**Base class:** `.badge`

**Soft variant:** `.badge.is-soft-primary`

```html
<span class="badge">Default</span>
<span class="badge is-soft-primary">New</span>
```

---

### Cards
**Base class:** `.card`

**Regions:** `.card-header`, `.card-body`, `.card-footer`

**Elevations:** `.elev-1`, `.elev-2`, `.elev-3`

```html
<article class="card elev-2">
  <header class="card-header"><h3>Card Title</h3></header>
  <div class="card-body">Body content…</div>
  <footer class="card-footer">
    <button class="btn is-primary">Action</button>
  </footer>
</article>
```

---

### Forms
**Wrappers:** `.field` (grid gap), `.label`, `.help`

**Controls:** `.input`, `.select`, `.textarea`

**Validation:** `.is-invalid` on `.input/.select/.textarea`

```html
<label class="field">
  <span class="label">Email</span>
  <input type="email" class="input" placeholder="you@example.com">
  <small class="help">We’ll never share your email.</small>
</label>

<input class="input is-invalid" placeholder="Required field">
```

---

### Switch
**Class:** `.switch` on an `input[type="checkbox"]`

```html
<label class="cluster items-center">
  <input type="checkbox" class="switch" checked>
  <span>Enable notifications</span>
</label>
```

---

### Navbar
**Classes:** `.navbar` → `.navbar-inner`

```html
<header class="navbar">
  <div class="navbar-inner">
    <strong>Brand</strong>
    <nav class="cluster">
      <a class="btn is-ghost" href="#">Docs</a>
      <a class="btn is-primary" href="#">Get Started</a>
    </nav>
  </div>
</header>
```

---

### Tabs
**Wrapper:** `.tabs`

**Tab:** `.tab` (use `aria-selected="true"` for active state)

```html
<div class="tabs">
  <button class="tab" aria-selected="true">Overview</button>
  <button class="tab">API</button>
  <button class="tab">Settings</button>
</div>
```

---

### Alerts
**Class:** `.alert`

**Variants:** `.is-success`, `.is-warning`, `.is-danger`

```html
<div class="alert is-success"><strong>Saved!</strong> Your changes were stored.</div>
```

---

### Modal (Dialog)
**Element:** `<dialog class="modal">`

**Subparts:** `.modal-header`, `.modal-body`, `.modal-footer`

```html
<button class="btn is-primary" onclick="m.showModal()">Open</button>
<dialog id="m" class="modal">
  <div class="modal-header"><strong>Title</strong></div>
  <div class="modal-body">Hello from NebulaCSS.</div>
  <div class="modal-footer">
    <button class="btn is-ghost" onclick="this.closest('dialog').close()">Cancel</button>
    <button class="btn is-primary" onclick="this.closest('dialog').close()">OK</button>
  </div>
</dialog>
```

---

### Tooltip
**Attribute:** `[data-tooltip]`

```html
<button class="btn" data-tooltip="I’m a tooltip!">Hover me</button>
```

---

### Glassmorphism Helper
**Class:** `.glass` — subtle blur and translucent surface.

```html
<div class="card glass p-4">Frosted panel</div>
```

---

## Utilities

NebulaCSS ships a pragmatic set of utilities under `@layer utilities`.

### Display
`hidden`, `block`, `inline`, `inline-block`, `flex`, `inline-flex`, `grid`

### Flexbox
`items-center`, `items-start`, `items-end`, `justify-center`, `justify-between`, `justify-start`, `justify-end`, `flex-col`, `flex-row`, `gap-1…6`

### Grid
`cols-1`, `cols-2`, `cols-3`, `cols-4`, `cols-6`, `cols-12`, `auto-rows`

### Spacing Utilities
Padding: `p-0/1/2/3/4/5/6`, `px-2/3/4/5`, `py-1/2/3/4`

Margin: `m-0/1/2/3/4`, `m-auto`, `mx-auto`, `mt-2/4`, `mb-2/4`

### Sizing
`w-full`, `h-full`, `min-h-screen`, `max-w-sm`, `max-w-md`, `max-w-lg`

### Borders & Radii
`rounded`, `rounded-sm`, `rounded-lg`, `rounded-xl`, `rounded-full`, `bordered`, `border-strong`

### Background / Text / Rings
`bg-surface`, `bg-surface-1`, `bg-surface-2`, `bg-primary`, `bg-soft-primary`, `text-primary`, `text-muted`, `text-invert`, `ring`

### Typography Utilities
`text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, `text-3xl`, `text-4xl`, `font-light`, `font-normal`, `font-medium`, `font-semibold`, `font-bold`, `text-center`, `text-left`, `text-right`

### Position
`relative`, `absolute`, `fixed`

### Shadows Utilities
`shadow-sm`, `shadow`, `shadow-lg`, `shadow-xl`

### Transitions
`transition`, `transition-fast`, `transition-slow`

### Animations
- Keyframes: `spin`, `pulse`, `float`
- Classes: `animate-spin`, `animate-pulse`, `animate-float`

### Utility Wrappers
- `.stack` → vertical rhythm: `> * + * { margin-block-start: var(--space-3) }`
- `.cluster` → horizontal wrap with gap and alignment

Example:
```html
<div class="stack">
  <h3>Section</h3>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</div>
```

---

## Responsive Variants

Use **prefixes** in class names (literal colons) to target breakpoints:
- `sm:` → `@media (min-width: 40rem)`
- `md:` → `@media (min-width: 48rem)`
- `lg:` → `@media (min-width: 64rem)`

Example:
```html
<div class="grid cols-1 sm:cols-2 md:cols-3 lg:cols-12 gap-3 lg:gap-6">
  ...
</div>
```

> **Note:** In plain HTML, colons in class names are fine. In JSX/CSS Modules, keep them as strings (e.g., `className="sm:cols-2"`).

---

## Container Queries

Opt-in by adding `.cq` to a parent container, then use `cq:` variants on children that should adapt to that container’s width.

- Enable: `.cq { container-type: inline-size; container-name: self }`
- Variants provided:
  - `cq:row` → `flex-direction: row`
  - `cq:cols-2` → `grid-template-columns: repeat(2, 1fr)`
  - `cq:cols-3` → `grid-template-columns: repeat(3, 1fr)`

Example:
```html
<div class="card cq p-4">
  <div class="flex flex-col cq:row gap-3">
    <div class="grid cols-1 cq:cols-2 gap-3">
      <div class="card p-3">A</div>
      <div class="card p-3">B</div>
    </div>
  </div>
</div>
```

---

## Color Helper Classes

Soft semantic surfaces for inline highlighting:
- `.soft-primary`, `.soft-success`, `.soft-warning`, `.soft-danger`

```html
<p class="soft-warning p-2 rounded">Heads up! Something needs your attention.</p>
```

---

## Print & Reduced Motion

- **Reduced motion**: Animations and transitions are disabled when `prefers-reduced-motion: reduce` is set by the user.
- **Print**: Shadows are removed for cleaner printouts.

---

## Theming & Overrides via Cascade Layers

**Override tokens**:
```css
@layer tokens {
  :root { --primary-h: 210; --primary-s: 90%; --primary-l: 56%; }
}
```

**Tweak components** without fighting specificity:
```css
@layer components {
  .btn.is-primary { border-radius: var(--radius-2xl); }
}
```

**Local themes** (scoped):
```html
<section class="theme-rose">
  <button class="btn is-primary">Rose Primary</button>
</section>
```

---

## Examples

### Starter Layout
```html
<div class="min-h-screen bg-surface">
  <header class="navbar">
    <div class="navbar-inner container">
      <strong>My App</strong>
      <div class="cluster">
        <a class="btn is-ghost" href="#">Docs</a>
        <a class="btn is-primary" href="#">Sign up</a>
      </div>
    </div>
  </header>

  <main class="container stack mt-4">
    <div class="grid gap-4 sm:cols-2 lg:cols-12">
      <article class="card elev-2 lg:col-span-8">
        <div class="card-header"><h2>Welcome</h2></div>
        <div class="card-body prose">
          <p>This page is styled with NebulaCSS.</p>
          <div class="alert is-success"><strong>Success:</strong> You’re all set!</div>
        </div>
        <div class="card-footer">
          <button class="btn">Default</button>
          <button class="btn is-accent">Accent</button>
          <button class="btn is-danger">Danger</button>
        </div>
      </article>

      <aside class="card lg:col-span-4">
        <div class="card-body stack">
          <label class="field">
            <span class="label">Email</span>
            <input class="input" type="email" placeholder="you@example.com">
            <small class="help">We’ll never share your email.</small>
          </label>
          <label class="field cluster items-center">
            <input class="switch" type="checkbox" checked>
            <span>Notifications</span>
          </label>
          <span class="badge is-soft-primary">New</span>
        </div>
      </aside>
    </div>
  </main>
</div>
```

---

## Roadmap
- Components: Table, Breadcrumbs, Accordion/Disclosure, Dropdown, Toasts, Progress, Skeletons, Pagination
- Utilities: More `gap-*`, aspect-ratio helpers, sticky and z-index helpers
- Tooling: Optional minified build, CSS custom properties docs site, theme generator

---

## Appendix: Quick Class Index

**Layout & Display:** `container`, `prose`, `hidden`, `block`, `inline`, `inline-block`, `flex`, `inline-flex`, `grid`, `auto-rows`

**Flex:** `items-center`, `items-start`, `items-end`, `justify-center`, `justify-between`, `justify-start`, `justify-end`, `flex-col`, `flex-row`, `gap-1…6`

**Grid:** `cols-1`, `cols-2`, `cols-3`, `cols-4`, `cols-6`, `cols-12`

**Spacing:** `p-0/1/2/3/4/5/6`, `px-2/3/4/5`, `py-1/2/3/4`, `m-0/1/2/3/4`, `m-auto`, `mx-auto`, `mt-2/4`, `mb-2/4`

**Sizing:** `w-full`, `h-full`, `min-h-screen`, `max-w-sm`, `max-w-md`, `max-w-lg`

**Borders/Radii:** `bordered`, `border-strong`, `rounded`, `rounded-sm`, `rounded-lg`, `rounded-xl`, `rounded-full`

**Color/Text:** `bg-surface`, `bg-surface-1`, `bg-surface-2`, `bg-primary`, `bg-soft-primary`, `text-primary`, `text-muted`, `text-invert`, `ring`

**Typography:** `text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, `text-3xl`, `text-4xl`, `font-light`, `font-normal`, `font-medium`, `font-semibold`, `font-bold`, `text-left`, `text-center`, `text-right`

**Position:** `relative`, `absolute`, `fixed`

**Shadows:** `shadow-sm`, `shadow`, `shadow-lg`, `shadow-xl`

**Motion:** `transition`, `transition-fast`, `transition-slow`, `animate-spin`, `animate-pulse`, `animate-float`

**Wrappers:** `stack`, `cluster`, `cq`

**Components:** `btn (+ variants/sizes)`, `badge (+ soft)`, `card (+ header/body/footer + elev)`, `field/label/input/select/textarea/help (+ is-invalid)`, `switch`, `navbar (+ navbar-inner)`, `tabs/tab`, `alert (+ variants)`, `modal (+ parts)`, `glass`, `sr-only`

