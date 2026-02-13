# 🔵 React 18/19 Master Development Standards

## 🏗 1. Architecture & Component Design

* **Functional Components:** Use arrow functions (`const MyComponent = () => ...`). **NEVER** use class components.
* **Logic Extraction:** Any logic involving `useEffect`, complex `useReducer`, or multi-step transitions **MUST** be extracted into a custom hook.
* **Type Safety:** * **NEVER use `any`.** Use strict TypeScript interfaces.
* **Strict Typing:** Always type function return types and parameters explicitly.
* **Literal Types:** Use literal types for return enforcement.
* **Exporting Types:** You **MUST** define and **EXPORT** an interface named `Props`.


* **Naming Convention:**
* **Variable Naming:** Never use single letters (a, i, b). Use meaningful, contextual names.
* **Boolean Naming:** Use clean prefixes like `is`, `has`, or `should`.
* **Contextual Loaders:** Avoid generic `isLoading`. Use `isUserDetailsLoading`, `isDataSubmitting`, etc.


* **Prop Decoupling:** Define props based on the **UI Role** rather than the Backend Domain.
* **Memoization Strategy:** Use `React.memo()`, `useCallback`, and `useMemo` for heavy data or stable references.
* **Fragments:** Use `<> </>` instead of unnecessary `<div>` wrappers.

## 🧠 2. Advanced Hooks & Side Effects

* **Concurrent UI & Transitions (`useTransition`):**
* **Rule:** Wrap non-urgent state updates (e.g., filtering a list, switching tabs) in `startTransition`.
* **UX:** Always use the `isPending` boolean to provide visual feedback (e.g., dimming the UI) while the transition is processing.


* **Declarative Loading (`Suspense`):**
* **Rule:** Every component using the `use()` hook or lazy loading **MUST** be wrapped in a `<Suspense>` boundary.
* **Fallback Strategy:** Fallbacks **MUST** be purposeful (Skeletons or themed Loaders). Never use a blank screen.


* **Modern Form Logic (`useActionState`):**
* **Rule:** Use `useActionState` (formerly `useFormState`) for all form submissions to manage state, errors, and pending status natively.
* **Logic:** Keep action functions pure and extracted from the UI component where possible.


* **The `use` API (React 19):** Use the `use()` hook to unwrap Promises or Contexts.
* **Hook Approach:** Always use the function approach when updating state based on previous state (e.g., `setCount(prev => prev + 1)`).
* **Effect & Cleanup:** You **MUST** clear all side effects in the `useEffect` cleanup. Always abort fetching requests using `AbortController` on unmount.
* **Readability Logic:** For conditions with many checks, assign the logic to a descriptively named constant.

## 🌐 3. API Communication & UX Logic

* **Data Fetching:** Prefer **Pattern A (Declarative)** with `use(promise)` and `<Suspense>`.
* **Search Optimization:** Always implement **debouncing** for search inputs.
* **Error Management:** Always explicitly manage errors on API requests. Use `try/catch` or Error Boundaries.
* **Visual Feedback:** Every async action **MUST** have a corresponding `isPending` or `is...Loading` state.
* **Interaction Safety:** **Disable buttons** immediately during pending requests.

## 🧪 4. Testing (Vitest + React Testing Library)

* **Persona:** Senior SDET. Focus on **Behavioral Testing**.
* **Selectors:** Use `data-test`, `data-cy`, or `data-test-id`. Priority: `getByRole` > `getByLabelText` > `data-test-id`.
* **Philosophy:**
* All test cases **MUST** start with the word **"should"**.
* **Isolation:** Treat child components as black boxes.


* **Event Simulation:** Use `@testing-library/user-event`. **NEVER** use `fireEvent`.
* **Mocking:** Use `vi.hoisted()` for `vi.fn()` inside `vi.mock()`.

## 🎨 5. Styling & Frameworks

* **Tailwind/CSS Libraries:** Use the library fully. Avoid custom CSS/SASS.
* **The !important Rule:** Avoid the usage of `!important` in CSS or framework classes.

## 🚦 6. Tooling, CI & Performance

* **Linter & Formatter:** Use **OXC/ESLint** and **Biome/Prettier**.
* **Package Manager:** Always ask which package manager (npm, pnpm, yarn) is preferred.
* **Git Standards:** Use **Commitlint** with conventional commit messages.
* **Logging:** Use a production-safe logger to avoid `console.log` in production.
* **Lighthouse Goals (100%):**
* **Semantic HTML:** Use `<main>`, `<nav>`, `<header>`, `<section>` strictly.
* **Accessibility (A11y):** 4.5:1 contrast, `aria-label` for icons, and keyboard navigation.
* **Performance:** Image `width`/`height` are required. Use `loading="lazy"` below fold.



## 📁 7. Asset Management & Vite Constraints

* **Vite Static Analysis:** No dynamic sub-folder paths in `new URL()`. Only the filename can be dynamic.
* **Structure:** `src/assets/icons/` and `src/assets/images/`. Use `BaseSvg` and `BaseImage` components.

## 🚪 8. The "Escape Hatch" (Justified Exceptions)

* **Protocol:** Rule violations require a `// @r-exception` comment, a justification, and isolation.
