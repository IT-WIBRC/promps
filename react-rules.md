# 🔵 React 18/19 Master Development Standards

## 🏗 1. Architecture & Component Design

* **Functional Components:** Use arrow functions (`const MyComponent = () => ...`). **NEVER** use class components.
* **Logic Extraction:** Any logic involving `useEffect`, complex `useReducer`, or multi-step transitions **MUST** be extracted into a custom hook (e.g., `useAuth.ts`).
* **Type Safety:** - **NEVER use `any`.** Use strict TypeScript interfaces for all data.
* You **MUST** define an interface named `Props` (or `ComponentProps`) and **EXPORT** it for external use.


* **Prop Decoupling:** Define props based on the **UI Role** (e.g., `title`) rather than the Backend Domain (e.g., `user_meta_display_name`).
* **Memoization Strategy:**
* Wrap expensive sub-components in `React.memo()`.
* Use `useCallback` for functions passed as props to memoized children.
* Use `useMemo` for heavy data transformations or stable object references.


* **Fragments:** Use `<> </>` instead of unnecessary `<div>` wrappers to maintain a flat DOM.

## 🧠 2. Advanced Hooks & Side Effects

* **The `use` API (React 19):** - Use the `use()` hook to unwrap Promises or Contexts directly in render.
* Unlike other hooks, `use()` **CAN** be used inside loops and conditional statements.
* Pair `use(promise)` with `<Suspense>` boundaries for declarative loading states.


* **State Management:** - **useReducer:** Use for complex state logic where the next state depends on the previous one.
* **useActionState:** Use for managing form state and pending transitions in React 19.
* **useRef:** Use for DOM access or persisting values that **MUST NOT** trigger a re-render.


* **Effect Cleanup:** You **MUST** clear all side effects in the `useEffect` cleanup return:
* `clearTimeout()` / `clearInterval()`.
* `window.removeEventListener()`.
* Abort pending API requests using `AbortController`.



## 🌐 3. API Communication & UX Logic

* **Data Fetching:** - **Pattern A (Declarative):** Pass a promise to a component and unwrap it with `use(promise)`.
* **Pattern B (Imperative):** Use `useEffect` with an empty dependency array for mount-only fetches.


* **Feedback States:** - Every async action **MUST** have a corresponding `isLoading` or `isPending` state.
* Implement **Skeletons** or **Loaders** to maintain a high-quality "Perceived Performance."


* **Interaction Safety:** - **Disable buttons** during pending requests to prevent race conditions.
* Use `useTransition` to mark non-urgent state updates as interruptible.



## 🧪 4. Testing (Vitest + React Testing Library)

* **Persona:** Senior SDET. Focus on **Behavioral Testing**.
* **Description Style:** All test cases **MUST** start with the word **"should"**.
* **Philosophy:** Test what the user sees. Do not test internal component state.
* **Selectors (Strict Order):** - **P1:** `screen.getByRole()` (Semantic/Accessibility first).
* **P2:** `screen.getByLabelText()` or `screen.getByPlaceholderText()`.
* **P3:** `data-testid` (Only as a last resort).


* **Event Simulation:** Use `@testing-library/user-event`. **NEVER** use `fireEvent`.
* **Mocking & Hoisting:** Use `vi.hoisted()` for any `vi.fn()` inside a `vi.mock()` block.
* **Isolation:** Always treat child components as black boxes; stub or mock external dependencies/hooks.

## 🚦 5. Tooling, CI & Performance
- **Linter & Formatter:** Use **OXC/ESLint** for logic and **Biome/Prettier** for formatting.
- **Git Standards:** Use **Commitlint** with conventional commit messages to maintain a clean, navigable history.
- **Lighthouse Goals (Target: 100% Across All Categories):**
  - **Semantic HTML:** Use `<main>`, `<nav>`, `<header>`, and `<section>` strictly. Avoid "div-soup" at all costs.
  - **Accessibility (A11y):** - Maintain a minimum **4.5:1** contrast ratio.
    - Every icon-only button **MUST** have an `aria-label`.
    - Every interactive element must be keyboard-navigable.
  - **Performance:** - Images must include `width` and `height` attributes to prevent Layout Shift (CLS).
    - Use `loading="lazy"` for all assets located below the fold.

## 📁 6. Asset Management & Vite Constraints

* **Vite Static Analysis:** You **CANNOT** use dynamic sub-folder paths in `new URL()`. Only the **filename** can be dynamic.
* **Directory Structure:** Separate assets into `src/assets/icons/` and `src/assets/images/`.
* **Base Components:** Use `BaseSvg` and `BaseImage` components to resolve paths using:
* `new URL(`../assets/icons/${props.name}.svg`, import.meta.url).href`.

## 🚪 7. The "Escape Hatch" (Justified Exceptions)
- **Rule:** Standards are 99.9% non-negotiable, but exceptions are allowed for performance edge cases or unique library integrations.
- **Protocol for Deviating:** If you must break a rule (e.g., using a manual DOM manipulation or a specific 'any' for a broken 3rd party type):
  1. **Comment Block:** You **MUST** include a `// @r-exception` comment.
  2. **Justification:** State **why** the standard was broken and **what** the risk is.
  3. **Isolation:** Keep the non-standard code contained within a single function or component to prevent "rule-creep" across the codebase.
