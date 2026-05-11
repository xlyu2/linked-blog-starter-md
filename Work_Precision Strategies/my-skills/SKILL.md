---
name: web-design-standards
version: "1.0"
description: >
  Defines color tokens, typography scale, spacing, border radius, shadow, and
  accessibility rules for web page development. Use when building or reviewing
  any web UI — components, pages, or layouts — to ensure visual consistency
  between Figma designs and production CSS. Covers semantic CSS variables
  (Light/Dark modes), font stacks, type scale, BEM naming, and anti-patterns.
  Load alongside figma-generate-library when bridging design tool output to code.
applies-to:
  - web components
  - landing pages
  - dashboards
  - design systems
  - CSS / HTML / React / Vue
tags:
  - color
  - typography
  - spacing
  - tokens
  - accessibility
  - css-variables
  - figma-to-code
disable-model-invocation: false
---

# Web Design Standards
**Version 1.0 · For Developers**

A practical reference for color, typography, spacing, and component tokens used across all web products. These standards ensure visual consistency between design tools (Figma) and production code.

---

## 1. Color System

### 1.1 Architecture

The color system uses a **two-layer model**:

| Layer | Purpose | Example |
|-------|---------|---------|
| **Primitives** | Raw values — never used directly in components | `blue-500: #3B82F6` |
| **Semantic tokens** | Alias to primitives — what components reference | `color.bg.primary → blue-500` |

Semantic tokens are **mode-aware** (Light / Dark). Primitives are not.

---

### 1.2 Primitive Palette

These are the raw color values. Do not use these directly in component styles — reference semantic tokens instead.

#### Neutrals
| Token | Hex | Usage |
|-------|-----|-------|
| `gray-50` | `#F9FAFB` | Page backgrounds (light) |
| `gray-100` | `#F3F4F6` | Surface backgrounds |
| `gray-200` | `#E5E7EB` | Borders, dividers |
| `gray-300` | `#D1D5DB` | Disabled borders |
| `gray-400` | `#9CA3AF` | Placeholder text |
| `gray-500` | `#6B7280` | Secondary text |
| `gray-600` | `#4B5563` | Body text (muted) |
| `gray-700` | `#374151` | Body text |
| `gray-800` | `#1F2937` | Headings |
| `gray-900` | `#111827` | Page background (dark) |
| `white` | `#FFFFFF` | — |
| `black` | `#000000` | — |

#### Brand — Blue
| Token | Hex |
|-------|-----|
| `blue-50` | `#EFF6FF` |
| `blue-100` | `#DBEAFE` |
| `blue-200` | `#BFDBFE` |
| `blue-400` | `#60A5FA` |
| `blue-500` | `#3B82F6` |
| `blue-600` | `#2563EB` |
| `blue-700` | `#1D4ED8` |
| `blue-900` | `#1E3A8A` |

#### Status — Green (Success)
| Token | Hex |
|-------|-----|
| `green-100` | `#DCFCE7` |
| `green-500` | `#22C55E` |
| `green-700` | `#15803D` |

#### Status — Red (Error / Danger)
| Token | Hex |
|-------|-----|
| `red-100` | `#FEE2E2` |
| `red-500` | `#EF4444` |
| `red-700` | `#B91C1C` |

#### Status — Yellow (Warning)
| Token | Hex |
|-------|-----|
| `yellow-100` | `#FEF9C3` |
| `yellow-500` | `#EAB308` |
| `yellow-700` | `#A16207` |

---

### 1.3 Semantic Color Tokens

Use these in all component and layout styles. The CSS variable name is the authoritative reference.

#### Background
| Token | CSS Variable | Light | Dark |
|-------|-------------|-------|------|
| Page background | `--color-bg-page` | `gray-50` | `gray-900` |
| Surface (card/panel) | `--color-bg-surface` | `white` | `gray-800` |
| Subtle (section fill) | `--color-bg-subtle` | `gray-100` | `gray-800` |
| Interactive (hover) | `--color-bg-hover` | `gray-100` | `gray-700` |
| Brand | `--color-bg-brand` | `blue-600` | `blue-500` |
| Brand subtle | `--color-bg-brand-subtle` | `blue-50` | `blue-900` |
| Danger | `--color-bg-danger` | `red-100` | `red-700` |
| Success | `--color-bg-success` | `green-100` | `green-700` |
| Warning | `--color-bg-warning` | `yellow-100` | `yellow-700` |

#### Text
| Token | CSS Variable | Light | Dark |
|-------|-------------|-------|------|
| Primary | `--color-text-primary` | `gray-900` | `white` |
| Secondary | `--color-text-secondary` | `gray-600` | `gray-400` |
| Tertiary / placeholder | `--color-text-tertiary` | `gray-400` | `gray-500` |
| Disabled | `--color-text-disabled` | `gray-300` | `gray-600` |
| On-brand (on blue bg) | `--color-text-on-brand` | `white` | `white` |
| Link | `--color-text-link` | `blue-600` | `blue-400` |
| Danger | `--color-text-danger` | `red-700` | `red-400` |
| Success | `--color-text-success` | `green-700` | `green-400` |

#### Border
| Token | CSS Variable | Light | Dark |
|-------|-------------|-------|------|
| Default | `--color-border-default` | `gray-200` | `gray-700` |
| Strong | `--color-border-strong` | `gray-300` | `gray-600` |
| Brand | `--color-border-brand` | `blue-500` | `blue-400` |
| Focus ring | `--color-border-focus` | `blue-500` | `blue-400` |
| Danger | `--color-border-danger` | `red-500` | `red-400` |

#### Interactive (Buttons & Controls)
| Token | CSS Variable | Light | Dark |
|-------|-------------|-------|------|
| Primary default | `--color-interactive-primary` | `blue-600` | `blue-500` |
| Primary hover | `--color-interactive-primary-hover` | `blue-700` | `blue-400` |
| Primary active | `--color-interactive-primary-active` | `blue-800` | `blue-300` |
| Destructive default | `--color-interactive-danger` | `red-600` | `red-500` |
| Disabled | `--color-interactive-disabled` | `gray-200` | `gray-700` |

---

### 1.4 CSS Implementation

```css
:root {
  /* --- Backgrounds --- */
  --color-bg-page:            #F9FAFB;
  --color-bg-surface:         #FFFFFF;
  --color-bg-subtle:          #F3F4F6;
  --color-bg-hover:           #F3F4F6;
  --color-bg-brand:           #2563EB;
  --color-bg-brand-subtle:    #EFF6FF;
  --color-bg-danger:          #FEE2E2;
  --color-bg-success:         #DCFCE7;
  --color-bg-warning:         #FEF9C3;

  /* --- Text --- */
  --color-text-primary:       #111827;
  --color-text-secondary:     #4B5563;
  --color-text-tertiary:      #9CA3AF;
  --color-text-disabled:      #D1D5DB;
  --color-text-on-brand:      #FFFFFF;
  --color-text-link:          #2563EB;
  --color-text-danger:        #B91C1C;
  --color-text-success:       #15803D;

  /* --- Borders --- */
  --color-border-default:     #E5E7EB;
  --color-border-strong:      #D1D5DB;
  --color-border-brand:       #3B82F6;
  --color-border-focus:       #3B82F6;
  --color-border-danger:      #EF4444;

  /* --- Interactive --- */
  --color-interactive-primary:        #2563EB;
  --color-interactive-primary-hover:  #1D4ED8;
  --color-interactive-primary-active: #1E40AF;
  --color-interactive-danger:         #DC2626;
  --color-interactive-disabled:       #E5E7EB;
}

[data-theme="dark"] {
  --color-bg-page:            #111827;
  --color-bg-surface:         #1F2937;
  --color-bg-subtle:          #1F2937;
  --color-bg-hover:           #374151;
  --color-bg-brand:           #3B82F6;
  --color-bg-brand-subtle:    #1E3A8A;

  --color-text-primary:       #FFFFFF;
  --color-text-secondary:     #9CA3AF;
  --color-text-tertiary:      #6B7280;
  --color-text-disabled:      #4B5563;
  --color-text-link:          #60A5FA;
  --color-text-danger:        #FCA5A5;
  --color-text-success:       #86EFAC;

  --color-border-default:     #374151;
  --color-border-strong:      #4B5563;
  --color-border-brand:       #60A5FA;
  --color-border-focus:       #60A5FA;
  --color-border-danger:      #EF4444;

  --color-interactive-primary:        #3B82F6;
  --color-interactive-primary-hover:  #60A5FA;
  --color-interactive-primary-active: #93C5FD;
  --color-interactive-disabled:       #374151;
}
```

> **Rule**: Never hardcode a hex value in a component style. Always use a `var(--color-*)` reference.

---

## 2. Typography

### 2.1 Font Stack

| Role | Font Family | Fallback |
|------|------------|---------|
| **Display / Headings** | `"Inter"` | `ui-sans-serif, system-ui, sans-serif` |
| **Body** | `"Inter"` | `ui-sans-serif, system-ui, sans-serif` |
| **Monospace / Code** | `"JetBrains Mono"` | `"Fira Code", ui-monospace, monospace` |

> Load from Google Fonts:
> ```html
> <link rel="preconnect" href="https://fonts.googleapis.com">
> <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
> ```

---

### 2.2 Type Scale

| Token | CSS Variable | Size | Line Height | Weight | Usage |
|-------|-------------|------|-------------|--------|-------|
| `display-2xl` | `--text-display-2xl` | 72px / 4.5rem | 1.1 | 700 | Hero headlines |
| `display-xl` | `--text-display-xl` | 60px / 3.75rem | 1.15 | 700 | Landing page titles |
| `display-lg` | `--text-display-lg` | 48px / 3rem | 1.2 | 700 | Section heroes |
| `heading-xl` | `--text-heading-xl` | 36px / 2.25rem | 1.25 | 700 | Page titles (H1) |
| `heading-lg` | `--text-heading-lg` | 30px / 1.875rem | 1.3 | 600 | Section headings (H2) |
| `heading-md` | `--text-heading-md` | 24px / 1.5rem | 1.35 | 600 | Sub-sections (H3) |
| `heading-sm` | `--text-heading-sm` | 20px / 1.25rem | 1.4 | 600 | Card headings (H4) |
| `heading-xs` | `--text-heading-xs` | 18px / 1.125rem | 1.45 | 600 | Small headings (H5) |
| `body-lg` | `--text-body-lg` | 18px / 1.125rem | 1.6 | 400 | Lead paragraph, intro text |
| `body-md` | `--text-body-md` | 16px / 1rem | 1.6 | 400 | Default body text |
| `body-sm` | `--text-body-sm` | 14px / 0.875rem | 1.55 | 400 | Secondary copy, captions |
| `body-xs` | `--text-body-xs` | 12px / 0.75rem | 1.5 | 400 | Timestamps, meta text |
| `label-lg` | `--text-label-lg` | 16px / 1rem | 1.25 | 500 | Form labels |
| `label-md` | `--text-label-md` | 14px / 0.875rem | 1.25 | 500 | Button text, tags |
| `label-sm` | `--text-label-sm` | 12px / 0.75rem | 1.25 | 500 | Badges, chips |
| `code-md` | `--text-code-md` | 14px / 0.875rem | 1.6 | 400 | Inline and block code |
| `code-sm` | `--text-code-sm` | 12px / 0.75rem | 1.6 | 400 | Small code snippets |

---

### 2.3 CSS Implementation

```css
:root {
  /* Font Families */
  --font-sans:  "Inter", ui-sans-serif, system-ui, sans-serif;
  --font-mono:  "JetBrains Mono", "Fira Code", ui-monospace, monospace;

  /* Display */
  --text-display-2xl-size:        4.5rem;
  --text-display-2xl-line-height: 1.1;
  --text-display-2xl-weight:      700;

  --text-display-xl-size:         3.75rem;
  --text-display-xl-line-height:  1.15;
  --text-display-xl-weight:       700;

  --text-display-lg-size:         3rem;
  --text-display-lg-line-height:  1.2;
  --text-display-lg-weight:       700;

  /* Headings */
  --text-heading-xl-size:         2.25rem;
  --text-heading-xl-line-height:  1.25;
  --text-heading-xl-weight:       700;

  --text-heading-lg-size:         1.875rem;
  --text-heading-lg-line-height:  1.3;
  --text-heading-lg-weight:       600;

  --text-heading-md-size:         1.5rem;
  --text-heading-md-line-height:  1.35;
  --text-heading-md-weight:       600;

  --text-heading-sm-size:         1.25rem;
  --text-heading-sm-line-height:  1.4;
  --text-heading-sm-weight:       600;

  --text-heading-xs-size:         1.125rem;
  --text-heading-xs-line-height:  1.45;
  --text-heading-xs-weight:       600;

  /* Body */
  --text-body-lg-size:            1.125rem;
  --text-body-lg-line-height:     1.6;
  --text-body-lg-weight:          400;

  --text-body-md-size:            1rem;
  --text-body-md-line-height:     1.6;
  --text-body-md-weight:          400;

  --text-body-sm-size:            0.875rem;
  --text-body-sm-line-height:     1.55;
  --text-body-sm-weight:          400;

  --text-body-xs-size:            0.75rem;
  --text-body-xs-line-height:     1.5;
  --text-body-xs-weight:          400;

  /* Labels */
  --text-label-lg-size:           1rem;
  --text-label-lg-line-height:    1.25;
  --text-label-lg-weight:         500;

  --text-label-md-size:           0.875rem;
  --text-label-md-line-height:    1.25;
  --text-label-md-weight:         500;

  --text-label-sm-size:           0.75rem;
  --text-label-sm-line-height:    1.25;
  --text-label-sm-weight:         500;

  /* Code */
  --text-code-md-size:            0.875rem;
  --text-code-md-line-height:     1.6;
  --text-code-md-weight:          400;

  --text-code-sm-size:            0.75rem;
  --text-code-sm-line-height:     1.6;
  --text-code-sm-weight:          400;
}
```

**Utility class pattern** (if not using a framework):

```css
.text-heading-xl {
  font-family: var(--font-sans);
  font-size: var(--text-heading-xl-size);
  line-height: var(--text-heading-xl-line-height);
  font-weight: var(--text-heading-xl-weight);
  color: var(--color-text-primary);
}

.text-body-md {
  font-family: var(--font-sans);
  font-size: var(--text-body-md-size);
  line-height: var(--text-body-md-line-height);
  font-weight: var(--text-body-md-weight);
  color: var(--color-text-primary);
}

code, pre, .text-code-md {
  font-family: var(--font-mono);
  font-size: var(--text-code-md-size);
  line-height: var(--text-code-md-line-height);
}
```

---

## 3. Spacing

All spacing values follow a **4px base grid**.

| Token | CSS Variable | Value | Typical Use |
|-------|-------------|-------|-------------|
| `spacing-px` | `--spacing-px` | 1px | Fine borders |
| `spacing-0.5` | `--spacing-0-5` | 2px | Icon gaps |
| `spacing-xs` | `--spacing-xs` | 4px | Tight padding |
| `spacing-sm` | `--spacing-sm` | 8px | Inner component padding |
| `spacing-md` | `--spacing-md` | 16px | Default gap |
| `spacing-lg` | `--spacing-lg` | 24px | Section padding |
| `spacing-xl` | `--spacing-xl` | 32px | Card padding |
| `spacing-2xl` | `--spacing-2xl` | 48px | Layout section gaps |
| `spacing-3xl` | `--spacing-3xl` | 64px | Page-level vertical rhythm |
| `spacing-4xl` | `--spacing-4xl` | 96px | Hero sections |

```css
:root {
  --spacing-px:   1px;
  --spacing-0-5:  2px;
  --spacing-xs:   4px;
  --spacing-sm:   8px;
  --spacing-md:   16px;
  --spacing-lg:   24px;
  --spacing-xl:   32px;
  --spacing-2xl:  48px;
  --spacing-3xl:  64px;
  --spacing-4xl:  96px;
}
```

---

## 4. Border Radius

| Token | CSS Variable | Value | Usage |
|-------|-------------|-------|-------|
| `radius-none` | `--radius-none` | 0px | Square elements |
| `radius-xs` | `--radius-xs` | 2px | Badges, tags |
| `radius-sm` | `--radius-sm` | 4px | Buttons, inputs |
| `radius-md` | `--radius-md` | 8px | Cards |
| `radius-lg` | `--radius-lg` | 12px | Modals, panels |
| `radius-xl` | `--radius-xl` | 16px | Large containers |
| `radius-2xl` | `--radius-2xl` | 24px | Feature cards |
| `radius-full` | `--radius-full` | 9999px | Pills, avatars |

```css
:root {
  --radius-none: 0px;
  --radius-xs:   2px;
  --radius-sm:   4px;
  --radius-md:   8px;
  --radius-lg:   12px;
  --radius-xl:   16px;
  --radius-2xl:  24px;
  --radius-full: 9999px;
}
```

---

## 5. Shadow

| Token | CSS Variable | Value | Usage |
|-------|-------------|-------|-------|
| `shadow-xs` | `--shadow-xs` | `0 1px 2px 0 rgb(0 0 0 / 0.05)` | Input fields |
| `shadow-sm` | `--shadow-sm` | `0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1)` | Dropdowns |
| `shadow-md` | `--shadow-md` | `0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1)` | Cards |
| `shadow-lg` | `--shadow-lg` | `0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1)` | Modals |
| `shadow-xl` | `--shadow-xl` | `0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1)` | Popovers |
| `shadow-focus` | `--shadow-focus` | `0 0 0 3px rgb(59 130 246 / 0.45)` | Focus rings |

---

## 6. Accessibility Rules

| Rule | Requirement |
|------|-------------|
| **Text contrast** | Minimum 4.5:1 for body text (WCAG AA) |
| **Large text contrast** | Minimum 3:1 for headings ≥ 18px bold or ≥ 24px regular |
| **Interactive contrast** | Minimum 3:1 for UI component boundaries |
| **Focus visibility** | Always use `--shadow-focus` on `:focus-visible`, never remove outline entirely |
| **Minimum touch target** | 44×44px for interactive elements on touch devices |
| **Disabled state** | Use `--color-text-disabled` and `--color-interactive-disabled`; never rely on color alone |

```css
/* Required focus style — never suppress without replacement */
:focus-visible {
  outline: none;
  box-shadow: var(--shadow-focus);
}
```

---

## 7. Naming Conventions

### CSS Variables

All variables follow the pattern: `--{category}-{subcategory}-{variant}`

```
--color-bg-primary
--color-text-secondary
--color-border-default
--text-heading-xl-size
--spacing-md
--radius-sm
```

### Component Class Names (BEM-aligned)

```
.btn                      /* Block */
.btn--primary             /* Modifier */
.btn--sm                  /* Size modifier */
.btn--disabled            /* State modifier */
.btn__icon                /* Element */
.card
.card--elevated
.card__header
.card__body
.input
.input--error
.input__label
.input__hint
```

---

## 8. Anti-Patterns

These are prohibited in production code:

- ❌ Hardcoding any hex color value in component styles — always use `var(--color-*)`
- ❌ Using primitive tokens (e.g. `--blue-500`) directly in component styles — use semantic tokens
- ❌ Setting `outline: none` on focused elements without a replacement focus indicator
- ❌ Using `px` for font sizes in the root element — use `rem` to respect browser zoom
- ❌ Line heights below 1.4 for body text (hurts readability)
- ❌ Using color alone to convey status — always pair with a label, icon, or pattern
- ❌ Adding inline `style` attributes with hardcoded values (except dynamic JS-driven values)
- ❌ Creating new one-off colors outside the palette — extend the primitives first, then add a semantic token

---

## 9. Figma ↔ Code Token Mapping

Figma variable names map directly to CSS variables using this convention:

| Figma Variable | CSS Variable |
|---------------|-------------|
| `color/bg/primary` | `--color-bg-primary` |
| `color/text/secondary` | `--color-text-secondary` |
| `color/border/default` | `--color-border-default` |
| `spacing/md` | `--spacing-md` |
| `radius/sm` | `--radius-sm` |
| `typography/body/font-size` | `--text-body-md-size` |

Slash separators in Figma become hyphens in CSS. The `var()` wrapper is always required in CSS.

---

*Maintained by the Design Systems team. For additions or changes, open a PR against this document.*
