# Design System, UX & Lighthouse Standards

## 1. Visual Hierarchy & "The Star" Strategy

* **The Focal Point (The Star):** Every page or major section **MUST** have one "Star" (e.g., a high-fidelity 3D render, a complex mesh gradient, or an interactive hero element).
* **Visual Rhyming:** Use the "Seed" method. If the "Star" or Logo uses a specific geometric property (e.g., a 15° slant or a specific corner radius), you **MUST** repeat that property in sub-components like buttons, icon containers, and image masks.
* **The 50ms Halo Effect:** The Hero section is non-negotiable. It must use bespoke assets. **NEVER** use generic, unedited stock photos. If a custom asset isn't available, use abstract CSS-driven gradients or high-end typography layouts.
* **Hierarchy of Opacity:** Do not use the same gray for all secondary text.
* **Primary (H1, H2, Key Labels):** 100% Opacity.
* **Secondary (Body, Sub-headers):** 87% Opacity (High emphasis).
* **Tertiary (Meta-data, Captions):** 60% Opacity (Medium emphasis).
* **Disabled/Quaternary:** 38% Opacity.

## 2. Geometry, Spacing & Typography

* **The Rule of Eights (Linear Algebra of UI):** All `gap`, `padding`, `margin`, and `height/width` increments **MUST** follow the $8n$ formula (8, 16, 24, 32, 40, 48, 56, 64, 80, 96). No exceptions for "visual tweaking."
* **The Anchor Font Strategy:** * **Headline Anchor:** Choose one high-character font (Serif or Display).
* **Supporting Body:** Choose a highly legible Sans-Serif.
* **Contrast:** Ensure a distinct difference in weight or width (e.g., Condensed Headline + Wide Body).


* **Border Radius System:** * Small (Buttons/Inputs): **8px**.
* Medium (Cards/Dropdowns): **12px**.
* Large (Modals/Hero Containers): **16px or 24px**.


* **Touch Targets:** Interactive elements **MUST** be at least **48x48px** with a minimum **8px** gap between targets to prevent "fat-finger" errors.

## 3. Cognitive Load & Motion Psychology

* **Cognitive Fluency:** Maintain "Mental Models." Do not move the Search bar or User Profile from expected industry positions (e.g., Top Right/Center).
* **Whitespace as Luxury:** Increase `section` padding by **1.5x** what feels "normal" to evoke a premium, uncluttered brand feel (The "Hermes" Effect).
* **Peak-End Interactions:** * **The Peak:** The moment of action (Button Click) must trigger immediate feedback (Scale down 95%, subtle color shift, or haptic sound).
* **The End:** The success state must be "Alive" (e.g., a checkmark that draws itself or a smooth toast entry).


* **Anti-Rage Click Logic:** Use `useTransition` (React 19) to ensure the UI remains responsive during heavy updates. Every async trigger **MUST** dim the background or show a progress bar within **100ms**.

## 4. Technical Performance (Lighthouse 100/100)

* **CLS Prevention (Layout Stability):** * Images and Iframes **MUST** have explicit `width` and `height` attributes.
* Dynamic content **MUST** be wrapped in a container with a `min-height` or a `Skeleton Loader` to reserve space.


* **Semantic SEO:** * Strictly use `<main>`, `<nav>`, `<header>`, `<footer>`, and `<section>`.
* `<h1>` is restricted to **one per page**. Headings must follow a strict tree: `h1 > h2 > h3`.

* **Accessibility (A11y):**
* Minimum contrast ratio: **4.5:1**.
* Every `<button>` without text **MUST** have an `aria-label`.
* Forms **MUST** have associated `<label>` tags (even if visually hidden via `sr-only`).

* **Asset Loading:** * Above fold: `loading="eager"` + `fetchpriority="high"`.
* Below fold: `loading="lazy"`.

## 5. Modern 2026 Trends

* **Barely-There UI:** For technical tools, use ultra-thin borders (0.5px), monospaced "Spaceship" labels, and data-driven graphs over icons.
* **Wabi-Sabi (The Human Touch):** Include one intentional "imperfection" (e.g., a hand-drawn underline, a paper-grain texture, or an asymmetrical layout element) to prove the site isn't "AI-generated-soup."
* **Sonic Feedback:** Implement subtle "Micro-clicks" for high-value interactions (Submit, Toggle, Delete).

