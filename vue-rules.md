# 🟢 Vue.js 3 Master Development Standards

## 🏗 1. Architecture & Component Design
- **Reactivity Model:** Use `<script setup>` and Composition API exclusively. **NEVER** use the Options API.
- **Component Persona:** Treat every component as a reusable library item.
- **Naming Convention:** - Layout or single-instance components **MUST** start with the `The` prefix (e.g., `TheNavbar.vue`, `TheFooter.vue`).
  - Use PascalCase for file names and component usage in templates.
- **Dumb Templates:** Templates must contain zero logic. All transformations, conditional checks, or formatting must live in `computed()` properties.
- **Prop Decoupling:** - Define props based on the **UI Role**, not the Backend Domain. Use `title` instead of `userDisplayName`.
  - **NEVER** copy props into local `ref` state unless the component is intended to "diverge" from the source.
- **Type Safety:** - You **MUST** define an interface named `Props`.
  - You **MUST** export this interface so it can be used externally by parents or test files.
  - Use type-based `defineEmits<{ (e: 'change', id: number): void }>` for strict event typing.

## 🧠 2. Composables (The AlexOp Standard)
- **Single Responsibility:** One composable = One feature. (e.g., `useAuth`, `useToggle`).
- **Return Pattern:** Always return a plain object (e.g., `return { data, execute }`).
- **Context Guarding:** If a composable uses `inject`, it must check if the value is null/undefined and throw a specific developer-friendly Error if the Provider is missing.
- **State Preservation:** Use `toRefs` when returning reactive objects to ensure destructuring doesn't break reactivity.

## 🧪 3. Testing (Vitest + @vue/test-utils)
- **Persona:** You are a Senior SDET. Tests are non-negotiable.
- **Isolation (Black Box):** - Always use `shallowMount` or explicit `global.stubs` for child components. 
  - **NEVER** allow a child component to be fully rendered in a unit test.
- **Selectors:** Use **ONLY** `data-test` or `data-cy` attributes. Do not use classes or HTML tags.
- **Mocking & Hoisting:**
  - When using `vi.fn()` inside `vi.mock()`, you **MUST** wrap the mock in `vi.hoisted()` to prevent undefined errors.
- **Routing:** - Use `RouterLinkStub` from `@vue-test-utils` to stub `RouterLink`.
  - **Assertion:** Explicitly test the `to` prop of the `RouterLinkStub` to verify the destination object/string.
- **Pinia:** Always use `createTestingPinia()` and provide initial state in the `initialState` object.
- **Execution Rules:**
  - **Call Tracking:** Always use `.toHaveBeenCalledTimes(n)`.
  - **Safety Check:** Always call `.exists()` on a wrapper before checking its props or triggering events.
  - **Strict Equality:** Use `toStrictEqual()` for all object and array assertions.
  - **Type Inference:** When using `findComponent` with a selector, use TypeScript inference to cast the return so props remain typed.
- **Cleanup:** - `afterEach`: Call `vi.clearAllMocks()`.
  - `afterAll`: Call `vi.resetAllMocks()` and reset any global timers.
- **Independence:** Each test must be isolated; resetting state between tests is mandatory.

## 🚦 4. Global Performance & UX (Lighthouse 100)
- **Semantic HTML:** Use `<main>`, `<nav>`, `<header>`, `<section>` strictly. No `div` soup.
- **Accessibility:**
  - Every icon-only button **MUST** have an `aria-label`.
  - Every input **MUST** have a linked `<label>` with a `for` attribute.
  - Maintain a minimum **4.5:1** contrast ratio.
- **Performance:** - Images must have `width`, `height`, and `loading="lazy"` (if below fold).
  - Use `font-display: swap` for any custom fonts.
