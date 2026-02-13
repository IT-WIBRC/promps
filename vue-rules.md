# 🟢 Vue.js 3 Master Development Standards

## 🏗 1. Architecture & Component Design

* **Reactivity Model:** Use `<script setup>` and Composition API exclusively. **NEVER** use the Options API or access the internal instance via `vm`.
* **Type Safety:** * **NEVER use `any`.** Use strict TypeScript interfaces for all data structures.
* **Strict Typing:** Always type function return types and parameters explicitly.
* **Literal Types:** Use literal types (e.g., `'success' | 'error'`) for strict return enforcement.


* **Component Persona:** Treat every component as a reusable library item.
* **Naming Convention:**
* Layout/single-instance components **MUST** start with the `The` prefix (e.g., `TheNavbar.vue`).
* Use PascalCase for file names and component usage in templates.
* **Variable Naming:** Never use single letters (a, i, b). Use meaningful, contextual names.
* **Boolean Naming:** Use clear prefixes like `is`, `has`, or `should`.
* **Contextual Loaders:** Avoid generic `isLoading`. Use specific names like `isUserDetailsLoading` or `areProductsFetching`.


* **Dumb Templates:** Templates must contain zero logic. All transformations and complex conditions **MUST** live in the `<script>` as `computed()` properties.
* **Prop Decoupling:** Define props based on the **UI Role**, not the Backend Domain. **NEVER** copy props into local `ref` state unless the component is intended to "diverge."
* **Exporting Types:** You **MUST** define and **EXPORT** an interface named `Props`. Use type-based `defineEmits<{ (e: 'change', id: number): void }>` for strict event typing.
* **Inheritance Logic:** Use logic inheritance via nested composables and UI inheritance via "Base Component" strategy with `v-bind="$attrs"`.

## 🧠 2. Advanced Reactivity & Optimization

* **Data Structures:** Favor **Map** and **Set** over Arrays for high-frequency updates ( performance).
* **Keys in Loops:** When using `v-for`, **NEVER** use the array index as a key. Use unique IDs.
* **Efficient States:** Use `shallowRef` instead of `ref` for primitive loading states or large objects that don't need deep reactivity.
* **Readability Logic:** For conditions with multiple checks, assign the logic to a descriptively named variable or computed property (e.g., `const isUserEligibleForDiscount = ...`) to make the code "read like a book."
* **Watchers:** `watch` for specific dependency tracking; `watchEffect` for automatic multi-dependency tracking.
* **Cleanup:** You **MUST** clear all side effects in `onUnmounted()`:
* `clearTimeout()` / `clearInterval()`.
* `removeEventListener()`.
* Abort pending API requests using `AbortController`.



## 🌐 3. API Communication & UX Logic

* **Lifecycle Timing:** Always call API fetch methods inside `onBeforeMount()`.
* **Search Optimization:** Always implement **debouncing** for search inputs to reduce server load.
* **Error Management:** Always explicitly manage and catch errors on API requests. Use `try/catch` and provide user notifications.
* **Visual Feedback:** Use `isLoading` states, **Loaders**, or **Skeletons**. **Disable buttons** immediately upon request to prevent duplicate submissions.
* **Request Safety:** Always abort fetching requests using `AbortController` in case of unexpected component changes or unmounting.

## 🧪 4. Testing (Vitest + @vue/test-utils)

* **Persona:** Senior SDET. Tests are non-negotiable.
* **Selectors:** Use `data-test`, `data-cy`, or `data-test-id` directly on elements. NEVER use CSS classes or tags.
* **Isolation:** Treat child components as black boxes. Use `shallowMount` or stubs.
* **Stub Rule:** Stub child components without redefining them. Simply set the property to `true` in the `global.stubs` object.


* **Assertions:**
* All test cases **MUST** start with **"should"**.
* Check `.exists()` before triggering events.
* If a component has props, test **all props presence**, display, and logic-driven changes.


* **Mocking:** Use `vi.hoisted()` for `vi.fn()` inside `vi.mock()`. Use `createTestingPinia()` for state.
* **Routing:** Use `RouterLinkStub` and explicitly test the `to` prop.

## 🎨 5. Styling & Frameworks

* **Tailwind/CSS Libraries:** Use the library fully. Avoid custom CSS unless absolutely necessary.
* **The !important Rule:** Avoid the usage of `!important` in CSS or framework classes as much as possible.

## 🧠 6. Composables (The AlexOp Standard)

* **Structure:** One composable = One feature. Return a plain object.
* **Context Guarding:** Throw an error if `inject` fails to find a Provider.
* **State Preservation:** Use `toRefs` when returning reactive objects.

## 🚦 7. Tooling, CI & Performance

* **Linter & Formatter:** Use **OXC/ESLint** and **Biome/Prettier**.
* **Package Manager:** Always ask which package manager (npm, pnpm, yarn) is preferred before installation.
* **Logging:** Use a dedicated logger (e.g., `signale` or a custom wrapper) to prevent `console.log` from reaching the production environment.
* **Lighthouse Goals (100%):**
* **Semantic HTML:** Use `<main>`, `<nav>`, `<header>`, `<section>` strictly.
* **A11y:** Maintain **4.5:1** contrast. Use `aria-label` for icons. Keyboard navigation is mandatory.
* **Performance:** Image `width`/`height` are required. Use `loading="lazy"` below the fold.



## 📁 8. Asset Management & Vite Constraints

* **Vite Analysis:** No dynamic sub-folder paths in `new URL()`. Only the filename can be dynamic.
* **Structure:** `src/assets/icons/` and `src/assets/images/`. Use `BaseSvg` and `BaseImage` to resolve paths.

## 🚪 9. The "Escape Hatch"

* **Protocol:** Rule violations require a `// @v-exception` comment, a justification, and code isolation.
