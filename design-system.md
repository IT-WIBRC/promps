# 🎨 Design System, UX & Lighthouse Standards

## 📐 1. Visual Hierarchy & Geometry
- **Spacing (8pt Grid):** All `margin`, `padding`, and `gap` values **MUST** be multiples of 8 (8px, 16px, 24px, 32px, 48px, 64px).
- **Border Radius:** - Standard Components (Buttons, Inputs, Cards): **8px (0.5rem)**.
  - Modals/Large Containers: **12px or 16px**.
- **Touch Targets:** Interactive elements **MUST** be at least **48x48px** for mobile usability.
- **Typography:** - Use `rem` units for font sizes (never `px`).
  - Maintain a line-height of at least **1.5** for body text.

## 🌑 2. Colors & Theming
- **Dark Mode:** Every component **MUST** have a `dark:` variant.
- **OLED Optimization:** Use `#121212` or `#0f172a` for dark backgrounds instead of pure `#000`.
- **Contrast Ratio:** Strictly follow WCAG 2.1 AA. Normal text must have **4.5:1** contrast; large text **3:1**.
- **States:** Define explicit styles for: `:hover`, `:active`, `:focus-visible` (mandatory high-visibility outline), and `:disabled`.

## 🚀 3. Google Lighthouse (100/100 Strategy)
- **Layout Shift (CLS):** - **ALWAYS** provide `width` and `height` to `<img>` and `<iframe>`.
  - Use skeleton loaders or aspect-ratio boxes for loading content.
- **Performance (LCP/FCP):**
  - Use `loading="lazy"` for all images below the fold.
  - Optimize `alt` text for all images; use `alt=""` only for decorative items.
- **Semantic HTML:** - Use `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` strictly. 
  - Headings (`<h1>` to `<h6>`) must follow a logical nesting order (no skipping levels).

## 🌐 4. API & Error Handling
- **Resilience:** Every API call must have a **10s timeout**.
- **Loading States:** Components **MUST** show a loading indicator or skeleton while fetching.
- **Error States:** Components **MUST** show a user-friendly error message if a fetch fails.
