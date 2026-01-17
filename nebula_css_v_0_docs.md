# NebulaCSS v1.0 — Documentation

A tiny, highly‑customizable CSS framework built on **design tokens**, **cascade layers**, and **zero‑build theming**. Ships with polished **components**, **utilities**, **responsive variants**, and **container-query helpers**.

> **Version:** 1.0 · **License:** MIT · **Author:** ChatGPT · **Updated:** With 50+ new features, components, and utilities

---

## Table of Contents
- [Getting Started](#getting-started)
- [What's New in v1.0](#whats-new-in-v10)
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
  - [Progress Bar](#progress-bar)
  - [Breadcrumbs](#breadcrumbs)
  - [Accordion](#accordion)
  - [Pagination](#pagination)
  - [Spinner](#spinner)
  - [Divider](#divider)
  - [Callout](#callout)
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
  - [Advanced Utilities (v1.0)](#advanced-utilities-v10)
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

## What's New in v1.0

**50+ new features** including:

✨ **New Design Tokens:**
- Extended easing functions (`ease-in`, `ease-out`, `ease-in-out`, `bounce`)
- Z-index scale for consistent layering (`z-base`, `z-dropdown`, `z-modal`, etc.)
- Opacity scale utilities (`--opacity-0` through `--opacity-100`)
- Aspect ratio presets (`square`, `video`, `4-3`, `3-2`, `golden`)

🎨 **New Theme Palettes:**
- `.theme-forest` — green & purple palette
- `.theme-sunset` — orange & purple palette
- `.theme-midnight` — deep blue palette
- `.theme-lavender` — purple & gold palette
- `.theme-mint` — teal & pink palette

🧩 **New Button Variants:**
- `.is-loading` — loading state with spinner
- `.is-block` — full-width button
- `.is-outlined-primary/secondary` — outlined button styles
- `.is-link` — link-style button
- `.is-shadow` — elevated button with shadow
- `.is-xl` — extra large size
- `:disabled` state handling

📦 **New Card Features:**
- `.is-interactive` — hover lift effect
- `.is-flat` — no shadow variant
- `.is-bordered` — strong border variant
- `.is-divided` — enhanced divider styling
- `.elev-4` — extra shadow elevation

🏷️ **New Badge Variants:**
- Soft variants for all semantic colors (success, warning, danger)
- `.is-pill` — pill-shaped badge

📝 **New Form Components:**
- `.input-group` — combined input + button groups
- `.label.is-required` — required indicator
- Form validation states (`.is-valid`, `.is-invalid`, `:disabled`)

🔘 **New Switch Sizes:**
- `.is-sm` — small switch
- `.is-lg` — large switch

📊 **New Components:**
- **Progress Bar** (`.progress`, `.progress-bar`)
- **Breadcrumbs** (`.breadcrumbs`)
- **Accordion** (`.accordion-item`, `.accordion-header`, `.accordion-content`)
- **Pagination** (`.pagination`)
- **Spinner** (`.spinner`)
- **Divider** (`.divider`, `.divider.is-vertical`)
- **Callout** (`.callout` with semantic variants)

🎯 **Advanced Utilities (100+ new):**
- **Opacity:** Full scale from 0-100
- **Z-Index:** Consistent layering scale
- **Aspect Ratios:** Multiple preset ratios
- **Cursor:** Full cursor style suite
- **Overflow:** Complete overflow control
- **Scroll Behavior:** Smooth scrolling
- **Text Decoration:** Underline, overline, line-through, decoration styles
- **List Styles:** List style utilities
- **Whitespace:** Text wrapping controls
- **Word Break:** Text breaking utilities
- **User Select:** Selection control
- **Pointer Events:** Event handling utilities
- **Transforms:** Scale, rotate, skew, translate
- **Filters:** Blur, brightness, contrast, grayscale, invert, saturate
- **Backdrop Filters:** Blur, brightness effects
- **Border Width:** Granular border control
- **Flex Basis & Grow/Shrink:** Flexbox fine-tuning
- **Max Height:** Height constraints
- **Letter Spacing & Line Height:** Typography refinement
- **Gradient Backgrounds:** Preset gradients
- **Striped Patterns:** Repeating backgrounds

✨ **Enhanced Animations:**
- `bounce`, `shake`, `slideInUp`, `slideInDown`, `fadeIn`, `fadeOut`, `scaleIn`
- Corresponding utility classes

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

### Progress Bar
**Classes:** `.progress`, `.progress-bar`

**Variants:** `.is-success`, `.is-warning`, `.is-danger`

```html
<div class="progress">
  <div class="progress-bar" style="width: 65%"></div>
</div>

<div class="progress">
  <div class="progress-bar is-success" style="width: 100%"></div>
</div>
```

---

### Breadcrumbs
**Class:** `.breadcrumbs`

```html
<nav class="breadcrumbs">
  <a href="#">Home</a>
  <a href="#">Products</a>
  <a href="#">Category</a>
  <span>Current Page</span>
</nav>
```

---

### Accordion
**Classes:** `.accordion-item`, `.accordion-header`, `.accordion-content`

**State:** `.is-open` on `.accordion-item`

```html
<div class="accordion-item is-open">
  <div class="accordion-header">Accordion Title</div>
  <div class="accordion-content">Content goes here...</div>
</div>
```

---

### Pagination
**Class:** `.pagination`

**Modifiers:** `.is-active`, `.is-disabled`

```html
<nav class="pagination">
  <a class="is-disabled">← Previous</a>
  <a class="is-active">1</a>
  <a>2</a>
  <a>3</a>
  <a>Next →</a>
</nav>
```

---

### Spinner
**Class:** `.spinner`

```html
<div class="spinner"></div>
```

---

### Divider
**Classes:** `.divider`, `.divider.is-vertical`

```html
<div class="divider"></div>
<div style="display: flex; gap: 2rem;">
  <div>Left</div>
  <div class="divider is-vertical"></div>
  <div>Right</div>
</div>
```

---

### Callout
**Classes:** `.callout`, `.callout.is-info`, `.callout.is-success`, `.callout.is-warning`, `.callout.is-danger`

```html
<div class="callout is-info">
  <strong>Info:</strong> This is important information.
</div>

<div class="callout is-success">
  <strong>Success:</strong> Operation completed successfully.
</div>
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

## Advanced Utilities (v1.0)

NebulaCSS v1.0 adds 100+ advanced utilities:

### Opacity
`opacity-0`, `opacity-10`, `opacity-20`, `opacity-30`, `opacity-40`, `opacity-50`, `opacity-60`, `opacity-70`, `opacity-80`, `opacity-90`, `opacity-100`

### Z-Index
`z-base`, `z-dropdown`, `z-sticky`, `z-fixed`, `z-modal-backdrop`, `z-modal`, `z-tooltip`, `z-notification`

### Aspect Ratios
`aspect-square`, `aspect-video`, `aspect-4-3`, `aspect-3-2`, `aspect-golden`

### Cursor Styles
`cursor-auto`, `cursor-default`, `cursor-pointer`, `cursor-wait`, `cursor-text`, `cursor-move`, `cursor-not-allowed`, `cursor-grab`, `cursor-grabbing`

### Overflow Control
`overflow-visible`, `overflow-hidden`, `overflow-scroll`, `overflow-auto`, `overflow-x-auto`, `overflow-y-auto`

### Scroll Behavior
`scroll-smooth`, `scroll-auto`

### Text Decoration
`underline`, `overline`, `line-through`, `no-underline`, `decoration-solid`, `decoration-dashed`, `decoration-dotted`, `decoration-wavy`

### List Styles
`list-none`, `list-disc`, `list-decimal`, `list-inside`, `list-outside`

### Whitespace & Text Wrapping
`whitespace-normal`, `whitespace-nowrap`, `whitespace-pre`, `whitespace-pre-wrap`, `whitespace-pre-line`, `truncate`, `line-clamp-1`, `line-clamp-2`, `line-clamp-3`

### Word Breaking
`break-normal`, `break-words`, `break-all`

### User Selection
`select-none`, `select-text`, `select-all`, `select-auto`

### Pointer Events
`pointer-events-none`, `pointer-events-auto`

### Transforms
`scale-75`, `scale-90`, `scale-100`, `scale-110`, `scale-125`, `rotate-45`, `rotate-90`, `rotate-180`, `skew-x-12`, `skew-y-12`, `translate-x-full`, `translate-y-full`

### Filters
`blur`, `blur-sm`, `blur-lg`, `brightness-75`, `brightness-125`, `contrast-75`, `contrast-125`, `grayscale`, `grayscale-0`, `invert`, `saturate-50`, `saturate-150`

### Backdrop Filters
`backdrop-blur`, `backdrop-blur-sm`, `backdrop-blur-lg`, `backdrop-brightness-75`, `backdrop-brightness-125`

### Border Width
`border-0`, `border-1`, `border-2`, `border-4`, `border-t`, `border-r`, `border-b`, `border-l`

### Gap Utilities
`gap-0`, `gap-1…6`, `gap-7`, `gap-8`

### Flexbox Fine-tuning
`basis-full`, `basis-1-2`, `basis-1-3`, `basis-1-4`, `basis-2-3`, `basis-3-4`, `flex-grow`, `flex-grow-0`, `flex-shrink`, `flex-shrink-0`

### Height Constraints
`max-h-xs`, `max-h-sm`, `max-h-md`, `max-h-lg`, `max-h-xl`, `max-h-full`, `max-h-screen`, `min-h-0`, `min-h-full`

### Typography Refinement
`tracking-tighter`, `tracking-tight`, `tracking-normal`, `tracking-wide`, `tracking-wider`, `leading-3…10`, `leading-relaxed`, `leading-loose`

### Gradients & Patterns
`bg-gradient-primary`, `bg-gradient-secondary`, `bg-gradient-accent`, `stripe-primary`, `stripe-secondary`

### Advanced Animations
`animate-bounce`, `animate-shake`, `animate-slide-up`, `animate-slide-down`, `animate-fade-in`, `animate-fade-out`, `animate-scale-in`

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

**v1.0 Completed:**
- ✅ Breadcrumbs, Accordion/Disclosure, Progress, Pagination
- ✅ 100+ advanced utility classes (opacity, z-index, transforms, filters, etc.)
- ✅ Extended animations and easing functions
- ✅ Additional theme palettes

**Future Roadmap (v1.1+):**
- Table component with styling
- Dropdown & context menus
- Toast notifications
- Skeleton loaders
- Combobox / Select dropdown
- File input styling
- Drag-and-drop utilities
- Sticky positioning helpers
- Optional minified build
- CSS variables documentation site
- Interactive theme generator
- Component composition guide

---

## Appendix: Quick Class Index

**Layout & Display:** `container`, `prose`, `hidden`, `block`, `inline`, `inline-block`, `flex`, `inline-flex`, `grid`, `auto-rows`

**Flex:** `items-center`, `items-start`, `items-end`, `justify-center`, `justify-between`, `justify-start`, `justify-end`, `flex-col`, `flex-row`, `gap-1…6`

**Grid:** `cols-1`, `cols-2`, `cols-3`, `cols-4`, `cols-6`, `cols-12`

**Spacing:** `p-0/1/2/3/4/5/6`, `px-2/3/4/5`, `py-1/2/3/4`, `m-0/1/2/3/4`, `m-auto`, `mx-auto`, `mt-2/4`, `mb-2/4`

**Sizing:** `w-full`, `h-full`, `min-h-screen`, `max-w-sm`, `max-w-md`, `max-w-lg`

**Borders/Radii:** `bordered`, `border-strong`, `rounded`, `rounded-sm`, `rounded-lg`, `rounded-xl`, `rounded-full`

**Color/Text:** `bg-surface`, `bg-surface-1`, `bg-surface-2`, `bg-primary`, `bg-soft-primary`, `text-primary`, `text-muted`, `text-invert`, `ring`, `bg-gradient-*`

**Typography:** `text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, `text-3xl`, `text-4xl`, `font-light`, `font-normal`, `font-medium`, `font-semibold`, `font-bold`, `text-left`, `text-center`, `text-right`, `tracking-*`, `leading-*`

**Position:** `relative`, `absolute`, `fixed`, `z-base`, `z-dropdown`, `z-modal`, etc.

**Shadows:** `shadow-sm`, `shadow`, `shadow-lg`, `shadow-xl`

**Motion:** `transition`, `transition-fast`, `transition-slow`, `animate-spin`, `animate-pulse`, `animate-float`, `animate-bounce`, `animate-shake`, `animate-slide-*`, `animate-fade-*`, `animate-scale-in`

**Advanced (v1.0):** `opacity-*`, `scale-*`, `rotate-*`, `blur*`, `brightness-*`, `contrast-*`, `grayscale`, `invert`, `overflow-*`, `whitespace-*`, `truncate`, `line-clamp-*`, `cursor-*`, `pointer-events-*`, `select-*`, `aspect-*`, `max-h-*`, `min-h-*`

**Wrappers:** `stack`, `cluster`, `cq`

**Components:** `btn (+ variants/sizes)`, `badge (+ soft/pill)`, `card (+ elev/interactive/flat)`, `field/label/input-group/textarea/help`, `switch (+ sizes)`, `navbar (+ variants)`, `tabs/tab`, `alert (+ dismissible)`, `modal (+ sizes)`, `progress`, `breadcrumbs`, `accordion`, `pagination`, `spinner`, `divider`, `callout`, `glass`, `sr-only`

