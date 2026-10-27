---
name: anti-slop-frontend-design
description: Build clean, modern, professional web interfaces and frontend code without AI slop clichés. Use when the user asks to design, structure, or code websites, landing pages, UI components, dashboard interfaces, or frontend layouts in HTML/CSS, React, Tailwind, or Vue.
---

# Anti-Slop Frontend Design

Guide the design and implementation of modern, high-craft web interfaces. Eliminate generic AI-generated aesthetic tropes (purple glows, floating glass blobs, emoji bullet points, uniform card grids) in favor of editorial typography, spatial discipline, restrained palettes, and concrete functional UI.

## When to Use

- Designing or writing code for web pages, landing pages, dashboards, and UI components.
- Reviewing or refactoring frontend styling to improve visual hierarchy and readability.
- Selecting typography, spacing tokens, color palettes, and icon sets for web applications.

---

## 1. Core Visual Principles

### Strict Emoji Prohibition

- Never use emojis as bullet points, section accents, button decorators, or category badges (`🚀`, `⚡`, `💡`, `🔥`, `✨`).
- Use crisp inline SVGs with explicit stroke widths (1.5px or 2px) and `currentColor` inheritance from established icon libraries (such as Lucide, Phosphor, or Radix).
- Rely on typographic scale, subtle uppercase labels, and clean horizontal rules rather than decorative symbols.

### Color Palette Restraint

- Follow the 90/10 balance: 90% muted neutral canvas and card surfaces; 10% maximum for accent color, strictly reserved for interactive states (primary actions, active tabs, focus indicators).
- Ban generic AI gradients: do not default to cyan-to-purple (`from-cyan-500 to-indigo-500`), ambient background blur blobs (`blur-3xl bg-purple-500/20`), or glowing neon card borders.
- Dark mode canvases should use tinted neutrals (e.g., zinc `#09090b` or slate `#0b0f19`) rather than pure `#000000`.
- Light mode canvases should favor subtle bone or eggshell tones (`#F9F9FB`, `#F7F7F8`) over blinding pure white backgrounds.
- Single Tint Discipline: Use strictly one accent tint across an entire screen or view, reserved exclusively for active interactive affordances (primary buttons, active tabs, toggle switches, disclosure indicators).

### Typography & Readability

- Set body line measure strictly between 45 and 75 characters (`max-w-[65ch]` or `max-w-2xl`). Never allow body copy to stretch across wide viewports.
- Pair an intentional display typeface (sharp sans, clean monospace, or editorial serif) for headings with a readable neutral text face for body copy.
- Tighten heading tracking and leading (`tracking-tight leading-tight`), while giving body text comfortable line height (`leading-relaxed` or `1.6`).
- Dual-Mode Optical Type Sizing: Use wider tracking and open counters on small text and metadata (sub-20px) to prevent muddiness, and tighter tracking on large display headers (20px+) for compact authority.
- Build hierarchy through contrast of weight and font opacity (e.g., 100% white header vs. 60% white secondary copy), not by simply inflating font size.
- Use `text-wrap: balance` on multi-line headers and subtitles to eliminate orphan words and awkward line splits.

---

## 2. Layout & Spatial Architecture

### Break "Card Syndrome"

- Do not wrap every feature, paragraph, or stat into an identical rounded card.
- Use diverse structural rhythm:
- Asymmetric 2/3 and 1/3 splits.
- Bordered data tables and key-value lists.
- Hairline dividers (`1px solid rgba(255, 255, 255, 0.08)` or `border-zinc-200/80`) instead of floating box cards.
- Alternating horizontal media-and-copy bands.

### Inset-Grouped Surfaces & Continuous Curvature

- Inset-Grouped Surface Pattern: Group related list or setting items into structured rounded containers inset cleanly from outer edges, separated by hairline dividers that indent to match text baselines rather than cutting through leading icons.
- Continuous Curvature (Squircles): Where supported or applicable in design tokens, favor continuous superellipse corner curves over abrupt circular fillets to prevent tangent seams and achieve clean, molded edges.

### Elevation, Vibrancy & Borders

- Replace heavy single-point drop shadows (`shadow-2xl`) with hairline borders and multi-layered diffused shadows.
- Avoid uniform aggressive corner rounding everywhere (e.g., do not slap `rounded-3xl` on buttons, inputs, cards, and containers alike). Use proportional rounding (smaller radius on buttons/inputs, medium on cards).
- Dynamic Vibrancy and Translucent Layers: On frosted surfaces, use backdrop blurs paired with luminosity blend modes and variable opacity rather than flat, heavy tint blocks, allowing underlying layout color to filter through cleanly.

### Proportional Sidebar & Target Sizing

- Never undersize navigation items or utility buttons in desktop sidebars. Provide comfortable click targets (`h-10` or `py-2.5 px-3` with `text-sm`) and scaled bounding boxes for icons (e.g., `w-5 h-5` with `1.5px` stroke).
- Dim or hide count badges when they equal 0 to reduce scanning clutter.

### Status Indicators & Token Separation

- Keep dynamic system status (e.g., live state, connection pulses) visually separate from static technical specifications (e.g., cipher names, version tags).
- Never place dynamic status indicators inside pills dedicated to static spec labels (e.g., separate `[● Ready]` from `[AES-256-GCM]`).

---

## 3. Alerts, Banners & Global Notifications

### Avoid Full-Width Floating Warning Strips

- Never insert full-width, single-line floating warning strips or alert bars directly above main tables or primary content views (e.g., a massive yellow/amber bordered box with a warning triangle on the left and an action button shoved to the far right).
- Why this breaks good UI:
  - Visual Severance: It creates an arbitrary horizontal barricade across the page that visually disconnects top navigation/search controls from the primary data below it.
  - Saccadic Eye Strain: Forcing the user to read an alert message anchored to the far-left edge while shoving the call-to-action button to the opposite far-right margin creates an enormous gulf of dead space, requiring aggressive horizontal eye scanning.
  - Saturated Color Pollution: Saturated alert borders (such as muddy amber `#D97706` or dark yellow) pollute a neutral slate palette and draw excessive visual weight away from the core workspace.
- What to do instead:
  - Group security, health, or warning summaries into a dedicated compact metric card, an integrated tab filter (e.g., an inline badge `Vulnerable (134)` next to `All Items`), or a dedicated non-modal drawer/toast.
  - When inline banners are strictly required, keep them compact, group the text and the action button tightly together (`gap-x-4`), and maintain a bounded width rather than spanning full screen width.

---

## 4. Forms, Inputs & Browser Defaults

### Neutralize Autofill Color Hijacking

- In dark themes, explicitly override the native WebKit autofill styling to eliminate light-yellow background hijacking (`#FEF9C3`):
  ```css
  input:-webkit-autofill,
  input:-webkit-autofill:hover, 
  input:-webkit-autofill:focus,
  input:-webkit-autofill:active {
    -webkit-text-fill-color: var(--text-primary, #f4f4f5) !important;
    -webkit-box-shadow: 0 0 0px 1000px var(--surface-bg, #18181b) inset !important;
    box-shadow: 0 0 0px 1000px var(--surface-bg, #18181b) inset !important;
    transition: background-color 5000s ease-in-out 0s;
    caret-color: var(--text-primary, #f4f4f5);
  }
  ```

---

## 5. Modals & Dialogs

### Custom Modal Architecture (No Built-in Native Modals)

- Never use built-in browser dialogs (`window.alert()`, `window.confirm()`, unstyled HTML5 `<dialog>` defaults, or generic OS prompt boxes).
- Always build custom modal and overlay components from scratch:
  - Accessible backdrop scrim with soft blur (`bg-black/60 backdrop-blur-sm`).
  - Clear z-index layering, keyboard focus trap, and escape key listener.
  - Dedicated header, body, and action footer layout with hairline borders (`border-t border-zinc-800`).
  - Predictable, snappy entry/exit transitions (scale and opacity fade with ease-out timing).

---

## 6. Data Tables & List Views

### Grid Alignment & Header Parity

- Header columns must strictly match the layout grid of the data rows below them. Avoid grouping headers ambiguously across multiple distinct data points (e.g., do not label a column `Website & Actions` when action buttons sit on the opposite edge).
- Use an explicit CSS Grid layout for both header and rows to keep columns locked in vertical alignment across all screen sizes:
  ```html
  <!-- Header -->
  <div class="grid grid-cols-[minmax(240px,2fr)_minmax(180px,1.5fr)_minmax(200px,1.5fr)_80px] items-center px-4 py-2.5 text-xs font-mono uppercase tracking-wider text-zinc-500 border-b border-zinc-800">
    <div>Title / Identity</div>
    <div>Secret</div>
    <div>Website</div>
    <div class="text-right">Actions</div>
  </div>

  <!-- Row -->
  <div class="group grid grid-cols-[minmax(240px,2fr)_minmax(180px,1.5fr)_minmax(200px,1.5fr)_80px] items-center px-4 py-3 hover:bg-zinc-900/40 border-b border-zinc-800/60 transition-colors">
    <div class="truncate">...</div>
    <div>...</div>
    <div>...</div>
    <div class="text-right">...</div>
  </div>
  ```
- Right-align numeric columns and interactive action buttons; left-align text and labels.

### Density & Hairlines Over Card Fatigue

- Avoid wrapping every table or list entry inside an isolated, floating rounded card. Use continuous bordered tables with subtle 1px hairline dividers (`border-b border-zinc-800/60`).
- Conceal row action buttons (edit, delete) until row hover (`opacity-0 group-hover:opacity-100 transition-opacity`) to eliminate visual noise down long repetitive lists.

---

## 7. Page Headings, Document Titles & Copywriting

### Concise Page & Document Titles (`<title>` and Headings)

- Document `<title>` tags and top-level brand titles must never be long, bloated, or packed with marketing fluff (e.g., avoid `MyProduct - The Best Next-Gen Modern AI Solution For Teams`).
- The main index or root page title must strictly be just the brand/app name (e.g., `<title>Name</title>`).
- Sub-pages or key views must only append the specific functional state or context without unnecessary buzzwords:
  - `Name Login`
  - `Name Register`
  - `Name Files`
  - `Name Settings`
  - `Name Vault`
- Avoid buzzword mad-libs in body text ("Supercharge your workflow", "Empower your scale", "Seamless next-gen synergy").
- State the product or tool function plainly and directly in sentence 1.
- Display realistic UI artifacts: syntax-highlighted code blocks, real data tables, accurate keyboard shortcuts, or functional terminal snippets rather than fake, tilted abstract browser mockups.

---

## 8. Frontend Code Standards

- Include complete interactive states for all clickable elements: `:hover`, `:active`, and keyboard `:focus-visible` (e.g., `focus-visible:ring-2 focus-visible:ring-accent focus-visible:outline-none`).
- Keep micro-interactions fast and snappy: transitions between 120ms and 200ms using ease-out timing curves.
- Ensure all custom SVGs have `aria-hidden="true"` when decorative, or appropriate `aria-label` when acting as icon buttons.