# 🎨 Design System & UX Standards

## 📐 Visual Rules
- **Spacing:** Use an **8pt Grid** (multiples of 8px for margins/padding).
- **Buttons:** - Radius: Default **8px (0.5rem)**. 
  - Size: Minimum touch target **48x48px**.
- **Colors:** Support `dark:` mode for everything. Minimum contrast ratio **4.5:1**.

## 🚀 Performance (Lighthouse 100)
- **Images:** Explicit `width`/`height` to prevent CLS. Use `loading="lazy"` below the fold.
- **Semantic HTML:** Use `<main>`, `<nav>`, `<section>`, etc. No `div` soup.
- **A11y:** Every icon-only button needs an `aria-label`. Every input needs a `<label>`.
