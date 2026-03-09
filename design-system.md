# 🎨 Design System, UX & Lighthouse Standards

## 📐 1. Visual Hierarchy & Geometry

* **The "Star" & Visual Rhyming:** Identify one "Star" element per page. Repeat subtle motifs (shapes/angles) from the Star/Logo in icons, masks, or button details.
* **Spacing (8pt Grid):** All `margin`, `padding`, and `gap` values **MUST** be multiples of 8 (8px, 16px, 24px, 32px, 48px, 64px).
* **Border Radius:**
* Standard Components (Buttons, Inputs, Cards): **8px (0.5rem)**.
* Modals/Large Containers: **12px or 16px**.


* **Touch Targets:** Interactive elements **MUST** be at least **48x48px** for mobile usability.
* **Typography (Hierarchy of Opacity):**
* Use `rem` units (never `px`). Line-height: **1.5+**.
* **Opacity:** Headlines at **100%**, Sub-headers/Body at **70-87%**, Decorative at **50%**.



## 🌑 2. Colors & Theming

* **The 60-30-10 Rule:** Limit palettes to 3-4 colors. 1 Primary brand color, 1 Secondary text color, 1 Neutral background.
* **Dark Mode:** Every component **MUST** have a `dark:` variant.
* **OLED Optimization:** Use `#121212` or `#0f172a` instead of pure `#000`.
* **Contrast Ratio:** Strictly follow WCAG 2.1 AA. Normal text: **4.5:1**; Large text: **3:1**.
* **States:** Define explicit styles for: `:hover`, `:active`, `:focus-visible` (mandatory high-visibility outline), and `:disabled`.

## 🚀 3. Google Lighthouse (100/100 Strategy)

* **Layout Shift (CLS):** - **ALWAYS** provide `width` and `height` to `<img>` and `<iframe>`.
* Use **Skeleton Loaders** or aspect-ratio boxes for loading content to prevent jumps.


* **Performance (LCP/FCP):**
* Use `loading="lazy"` below the fold.
* Optimize `alt` text; use `alt=""` only for purely decorative items.


* **Semantic HTML:** - Use `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` strictly.
* Headings (`<h1>` to `<h6>`) must follow logical nesting (no skipping levels).



## 🌐 4. API & Error Handling

* **Resilience:** Every API call must have a **10s timeout**.
* **Loading States:** Components **MUST** show a loading indicator or skeleton while fetching.
* **Error States:** Components **MUST** show a user-friendly error message if a fetch fails.
* **Interaction Safety:** Disable buttons immediately upon click to prevent race conditions or "double-submits."
