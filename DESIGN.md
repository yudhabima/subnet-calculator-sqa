---
name: Clarity Learning
colors:
  surface: '#faf9fd'
  surface-dim: '#dbd9dd'
  surface-bright: '#faf9fd'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f4f3f7'
  surface-container: '#efedf1'
  surface-container-high: '#e9e7eb'
  surface-container-highest: '#e3e2e6'
  on-surface: '#1a1b1e'
  on-surface-variant: '#414754'
  inverse-surface: '#2f3033'
  inverse-on-surface: '#f1f0f4'
  outline: '#727785'
  outline-variant: '#c1c6d6'
  surface-tint: '#005bc0'
  primary: '#005bbf'
  on-primary: '#ffffff'
  primary-container: '#1a73e8'
  on-primary-container: '#ffffff'
  inverse-primary: '#adc7ff'
  secondary: '#006e2b'
  on-secondary: '#ffffff'
  secondary-container: '#93f59e'
  on-secondary-container: '#00722d'
  tertiary: '#bb1712'
  on-tertiary: '#ffffff'
  tertiary-container: '#df3429'
  on-tertiary-container: '#ffffff'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#d8e2ff'
  primary-fixed-dim: '#adc7ff'
  on-primary-fixed: '#001a41'
  on-primary-fixed-variant: '#004493'
  secondary-fixed: '#96f8a1'
  secondary-fixed-dim: '#7adb87'
  on-secondary-fixed: '#002108'
  on-secondary-fixed-variant: '#00531f'
  tertiary-fixed: '#ffdad5'
  tertiary-fixed-dim: '#ffb4a9'
  on-tertiary-fixed: '#410001'
  on-tertiary-fixed-variant: '#930004'
  background: '#faf9fd'
  on-background: '#1a1b1e'
  surface-variant: '#e3e2e6'
typography:
  display-lg:
    fontFamily: Roboto Flex
    fontSize: 3.5rem
    fontWeight: '600'
    lineHeight: 4rem
    letterSpacing: -0.02em
  display-lg-mobile:
    fontFamily: Roboto Flex
    fontSize: 2.25rem
    fontWeight: '600'
    lineHeight: 2.75rem
    letterSpacing: -0.015em
  headline-lg:
    fontFamily: Roboto Flex
    fontSize: 2rem
    fontWeight: '500'
    lineHeight: 2.5rem
    letterSpacing: -0.01em
  headline-lg-mobile:
    fontFamily: Roboto Flex
    fontSize: 1.5rem
    fontWeight: '500'
    lineHeight: 2rem
    letterSpacing: '0'
  headline-md:
    fontFamily: Roboto Flex
    fontSize: 1.375rem
    fontWeight: '500'
    lineHeight: 1.75rem
    letterSpacing: '0'
  headline-sm:
    fontFamily: Roboto Flex
    fontSize: 1.125rem
    fontWeight: '500'
    lineHeight: 1.5rem
    letterSpacing: '0'
  body-lg:
    fontFamily: Roboto Flex
    fontSize: 1rem
    fontWeight: '400'
    lineHeight: 1.5rem
    letterSpacing: 0.01em
  body-md:
    fontFamily: Roboto Flex
    fontSize: 0.875rem
    fontWeight: '400'
    lineHeight: 1.375rem
    letterSpacing: 0.01em
  body-sm:
    fontFamily: Roboto Flex
    fontSize: 0.75rem
    fontWeight: '400'
    lineHeight: 1.125rem
    letterSpacing: 0.02em
  label-lg:
    fontFamily: Roboto Flex
    fontSize: 0.875rem
    fontWeight: '500'
    lineHeight: 1.25rem
    letterSpacing: 0.015em
  label-md:
    fontFamily: Roboto Flex
    fontSize: 0.75rem
    fontWeight: '500'
    lineHeight: 1rem
    letterSpacing: 0.025em
  code-md:
    fontFamily: JetBrains Mono
    fontSize: 0.8125rem
    fontWeight: '400'
    lineHeight: 1.25rem
    letterSpacing: '0'
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 1.5rem
  gutter-sm: 1rem
  margin: 2rem
  margin-sm: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2.5rem
---

## Brand & Style

This design system delivers an intuitive, distraction-free environment for modern digital education. It reflects clarity, academic utility, and structural simplicity. The aesthetic pairs the systematic rigor of enterprise-grade productivity suites with approachable, human-centered details.

- **Design Style:** Modern Material-inspired minimalism. The system uses high white-space efficiency, neutral architectural surfaces, sharp semantic accents, and structured typography.
- **Target Audience:** Educators, researchers, and students navigating complex curriculums, assessments, interactive notebooks, and technical datasets.
- **Emotional Response:** Calm focus, institutional reliability, cognitive ease, and academic confidence.

## Colors

The palette establishes an open, hygienic learning surface. Structural hierarchy is maintained through soft gray gradations, reserving chromatic saturation for purposeful interactive triggers and validation states.

### Palette Architecture
- **Primary Accent (`#1A73E8`):** Anchors core actions, links, active tabs, and primary button fills. Hover state tightens to `#174EA6`. The low-contrast container tone `#E8F0FE` houses selected states and soft tags.
- **Success & Progression (`#188038`):** Conveys mastery, submitted states, and positive validation. Accompanied by `#E6F4EA` for container and alert backgrounds.
- **Critical & Error (`#D93025`):** Reserved strictly for incorrect assessments, validation errors, and destructive triggers. Accompanied by `#FCE8E6` for container backdrops.
- **Warning & In-Progress (`#F29900`):** Indicates pending assignments or incomplete criteria, paired with container tint `#FEF7E0`.
- **Canvas & Surface Tiering:**
  - `Surface 0 (Base Canvas):` `#FFFFFF`
  - `Surface 1 (Off-Canvas / Sidebars):` `#F8F9FA`
  - `Surface 2 (Segmented Trackers / Wells):` `#F1F3F4`
- **Text & Content Tiers:**
  - `Primary Text:` `#202124` (High contrast, headlines, active states)
  - `Secondary Text:` `#3C4043` (Body copy, primary metadata)
  - `Tertiary Text:` `#5F6368` (Captions, inactive icons, helper copy)
  - `Disabled / Placeholder:` `#70757A`
- **Structural Outlines:** Subtle, hairline dividing borders using `#DADCE0` (interactive/cards) and `#E0E2E6` (internal dividers).

## Typography

The typography centers on **Roboto Flex** for all UI surfaces, headlines, and instructional bodies to ensure exceptional readability, variable scaling, and a standard academic tone. 

- **Numerical & Data Readability:** For test scores, math formulas, line numbers, and tabular data, apply `JetBrains Mono` or enforce `font-variant-numeric: tabular-nums` to prevent horizontal shifting during score recalculations and timer ticks.
- **Vertical Rhythm:** Headings enforce tight line-heights without aggressive negative tracking to prioritize legibility over drama.
- **Hierarchy Rules:** Section titles rely on medium weight (`500`) instead of heavy bolds (`700`) to retain a light, non-coercive editorial environment.

## Layout & Spacing

The layout model uses an 8pt foundational baseline rhythm with a fluid 12-column responsive grid on desktop, scaling to 8 columns on tablet and 4 columns on mobile.

### Breakpoints & Adaptive Rules
- **Desktop (1280px+):** 12 columns, 24px gutters, fixed or dynamic side rails (256px navigation drawer). Max container width capped at 1440px for broad content and 840px for single-column reading modules.
- **Tablet (768px – 1279px):** 8 columns, 16px gutters, collapsible drawer navigation converting to an icon rail or top app bar.
- **Mobile (< 768px):** 4 columns, 16px gutters, 16px margin. Primary navigation shifts to a persistent bottom bar; dense educational tables switch to scrollable or card-stack alternatives.

### Spacing Philosophy
Layout gaps (`space-lg`, `space-xl`) keep content-heavy curriculums from feeling crowded. Compact spacings (`space-xs`, `space-sm`) are strictly isolated to atomic clusters (e.g., tag icons, score badges, label-to-input relations).

## Elevation & Depth

This design system avoids dark or heavy drop shadows, relying primarily on 1px crisp borders (`#DADCE0`), subtle surface color shifts, and diffuse ambient elevations.

- **Level 0 (Flat):** Used for main structural frames and base work areas. Background `#FFFFFF` or `#F8F9FA` with borders set to `#DADCE0`.
- **Level 1 (Card / Rest):** Subtle separation for individual learning cards and question items.
  - Border: `1px solid #DADCE0`
  - Shadow: `0 1px 2px 0 rgba(60, 64, 67, 0.08), 0 1px 3px 1px rgba(60, 64, 67, 0.04)`
- **Level 2 (Hover / Floating Item):** For interactive card states, course modules under cursor focus, and drop-down menus.
  - Border: `1px solid transparent`
  - Shadow: `0 2px 6px 2px rgba(60, 64, 67, 0.15), 0 1px 2px 0 rgba(60, 64, 67, 0.30)`
- **Level 3 (Modals / Overlays):** Dialogs, submission confirmations, full-page side-sheets.
  - Shadow: `0 8px 10px 1px rgba(60, 64, 67, 0.14), 0 3px 14px 2px rgba(60, 64, 67, 0.12), 0 5px 5px -3px rgba(60, 64, 67, 0.20)`
- **Tonal Layering Rule:** An elevated card must never nest another elevated card of equal elevation. Internal elements must use a recessed surface (`#F1F3F4`) with borderless boundaries.

## Shapes

The shape system blends friendly modern geometry with precise functionality. 

- **Base Radius (`rounded-md`, 0.5rem / 8px):** Applied to form controls, input elements, buttons, menu sheets, and contextual tooltips.
- **Large Radius (`rounded-xl`, 1rem / 16px):** Standard for main content cards, assignment modules, and dashboard analytics blocks.
- **Extra Large Radius (`rounded-2xl`, 1.5rem / 24px):** Reserved for hero banners, modals, and multi-step assessment containers.
- **Pill Shape (`rounded-full`):** Strictly used for interactive filter chips, status badges, and user avatars.

## Components

### Buttons
- **Primary Button:** `#1A73E8` solid fill, `#FFFFFF` text, `0.5rem` radius, `label-lg` font. Hover shifts to `#174EA6`. Active state uses `rgba(26, 115, 232, 0.12)` ripple/overlay.
- **Secondary (Tonal) Button:** `#E8F0FE` fill, `#1A73E8` text, borderless. Hover shifts to `#D2E3FC`.
- **Outlined Button:** `#FFFFFF` fill, `#1A73E8` text, `1px solid #DADCE0` border. Hover shifts background to `#F8F9FA`.
- **Text Button:** Transparent background, `#1A73E8` text, `0.5rem` radius. Hover background `#F1F3F4`.

### Chips & Filter Pills
- Fully rounded (`rounded-full`), height `32px`, font `label-md`.
- **Default:** `#FFFFFF` background, `1px solid #DADCE0` border, `#3C4043` text.
- **Active / Selected:** `#E8F0FE` background, `1px solid #1A73E8` border, `#1A73E8` text with leading checkmark icon.

### Form Inputs & Textareas
- Height `48px` (single-line), background `#FFFFFF`, border `1px solid #DADCE0`, radius `0.5rem`.
- Padding: `0 16px`. Label floats or rests above in `label-md` `#5F6368`.
- **Focus:** Border shifts to `2px solid #1A73E8`, inset outline suppressed.
- **Error State:** Border shifts to `2px solid #D93025`, trailing error icon, caption text in `#D93025`.

### Checkboxes & Radio Buttons
- 18px bounding box, 2px border radius for checkboxes, circle for radios.
- Unchecked: `#5F6368` border with `#FFFFFF` background.
- Checked: `#1A73E8` fill with `#FFFFFF` interior mark. Hover applies an 8px diffuse ripple `rgba(26, 115, 232, 0.08)`.

### Cards & Assignment Panels
- Standard card: Surface `#FFFFFF`, border `1px solid #DADCE0`, radius `1rem`, padding `1.5rem`.
- Hoverable learning module: Incorporates a 200ms transition to Elevation Level 2 and an optional `#1A73E8` left border strip (4px width).

### Educational Callouts & Assessment Banners
- **Success Banner:** `#E6F4EA` background, `#188038` text, left border `4px solid #188038`, radius `0.5rem`.
- **Feedback / Note Banner:** `#E8F0FE` background, `#1A73E8` text, left border `4px solid #1A73E8`, radius `0.5rem`.
- **Alert Banner:** `#FCE8E6` background, `#D93025` text, left border `4px solid #D93025`, radius `0.5rem`.