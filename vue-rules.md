# Vue.js 3 Master Development Standards

## 🏗 1. Architecture & Component Design

* **Reactivity Model:** Use `<script setup>` and Composition API exclusively. **NEVER** use the Options API or access the internal instance via `vm`.
* **Type Safety:** **NEVER use `any`.** Use strict TypeScript interfaces for all data structures.
* **Component Persona:** Treat every component as a reusable library item.
* **Naming Convention:** - Layout or single-instance components **MUST** start with the `The` prefix (e.g., `TheNavbar.vue`).
* Use PascalCase for file names and component usage in templates.


* **Dumb Templates:** Templates must contain zero logic. All transformations **MUST** live in `computed()` properties.
* **Prop Decoupling:** - Define props based on the **UI Role**, not the Backend Domain.
* **NEVER** copy props into local `ref` state unless the component is intended to "diverge."


* **Exporting Types:** You **MUST** define and **EXPORT** an interface named `Props` for every component.
* Use type-based `defineEmits<{ (e: 'change', id: number): void }>` for strict event typing.


* **Inheritance Logic:** Use logic inheritance via nested composables and UI inheritance via "Base Component" strategy with `v-bind="$attrs"`.

## 🧠 2. Advanced Reactivity & Optimization

* **Data Structures:** Favor **Map** and **Set** over Arrays for collections involving frequent lookups or uniqueness ( performance).
* **Computed Properties:** MUST be pure and free of side effects.
* **Watch vs. WatchEffect:** `watch` for specific dependency tracking/oldValue; `watchEffect` for automatic multi-dependency tracking.
* **Cleanup:** You **MUST** clear all side effects in `onUnmounted()`:
* `clearTimeout()` / `clearInterval()`.
* `removeEventListener()`.
* Stop manual watchers and call `.abort()` on pending `AbortController` requests.



## 🌐 3. API Communication & UX Logic

* **Lifecycle Timing:** Always call API fetch methods inside `onBeforeMount()` to initiate data retrieval before the DOM tree begins building.
* **Visual Feedback:** Use reactive `isLoading` states, **Loaders**, or **Skeletons** for all async actions.
* **Interaction Safety:** **Disable buttons** immediately when they trigger a request. Use visual indicators (cursors/spinners) to show processing.
* **Error Resilience:** Wrap all API calls in `try/catch` and provide explicit user notifications.

## 🧪 4. Testing (Vitest + @vue/test-utils)

* **Persona:** Senior SDET. Tests are non-negotiable.
* **Description Style:** All test cases **MUST** start with the word **"should"**.
* **Isolation (Black Box):** Treat sub-components as black boxes. Always use `shallowMount` or explicit stubs. **NEVER** allow child components to be interpreted/rendered.
* **Selectors:** Use **ONLY** `data-test` or `data-cy` attributes. NEVER use standard HTML elements or CSS classes as selectors.
* **Mocking & Hoisting:** Use `vi.hoisted()` for any `vi.fn()` declared inside a `vi.mock()` block to ensure accessibility before hoisting.
* **Routing:** - Do **NOT** create an entire vue-router history instance for unit tests.
* Use `RouterLinkStub`. **Assertion:** Test the `to` prop explicitly to ensure it fails if the destination changes.


* **Pinia:** Use `createTestingPinia()` for all state mocking.
* **Execution Rules:**
* Always call `.exists()` on an element or stubbed component before checking props or triggering events.
* If a component has props, test **all props presence**, their display, and how logic changes them.
* Use TypeScript inference (e.g., `wrapper.findComponent<typeof MyComp>`) when using selectors other than the component object to avoid type errors.
* Use `toStrictEqual()` for all object/array assertions and always verify `.toHaveBeenCalledTimes(n)`.


* **Cleanup:** `afterEach` -> `vi.clearAllMocks()`; `afterAll` -> `vi.resetAllMocks()` and reset timers.

## 🧠 5. Composables (The AlexOp Standard)

* **Structure:** One composable = One feature. Return a plain object.
* **Context Guarding:** Throw a developer-friendly Error if `inject` fails to find a Provider.
* **State Preservation:** Use `toRefs` when returning reactive objects to preserve reactivity during destructuring.

## 🚦 6. Tooling, CI & Performance

* **Linter & Formatter:** Use **OXC** or **ESLint** for linting and **Biome** or **Prettier** for formatting.
* **Git Standards:** Use **Commitlint** with conventional commit messages (feat, fix, docs, etc.).
* **CI Checking:** All linting, formatting, and tests **MUST** pass in the CI pipeline before merging.
* **Lighthouse:** Maintain **4.5:1** contrast, semantic HTML (`<main>`, `<nav>`, etc.), and `loading="lazy"` for below-the-fold images.

## 📁 7. Asset Management & Vite Constraints

* **Vite Static Analysis:** You **CANNOT** use dynamic sub-folder paths in `new URL()`. Only the **filename** can be dynamic.
* **Directory Structure:** Separate assets into `src/assets/icons/` and `src/assets/images/`.
* **Base Components:** Use `BaseSvg` and `BaseImage` components to resolve paths using the pattern: `new URL(`../assets/icons/${props.name}.svg`, import.meta.url).href`.

## 🚪 8. The "Escape Hatch" (Justified Exceptions)
- **Rule:** Standards are 99.9% non-negotiable, but exceptions are allowed for performance edge cases or unique library integrations.
- **Protocol for Deviating:** If you must break a rule (e.g., using a manual DOM manipulation or a specific 'any' for a broken 3rd party type):
  1. **Comment Block:** You **MUST** include a `// @v-exception` or `// @r-exception` comment.
  2. **Justification:** State **why** the standard was broken and **what** the risk is.
  3. **Isolation:** Keep the non-standard code contained within a single function or component to prevent "rule-creep" across the codebase.
