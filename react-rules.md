# 🔵 React 18+ Master Development Standards

## 🏗 1. Architecture & Component Design
- **Functional Components:** Use arrow functions (`const MyComponent = () => ...`). **NEVER** use class components.
- **Logic Extraction:** Any logic involving `useEffect`, complex `useMemo`, or multi-step state transitions **MUST** be extracted into a custom hook (e.g., `useAuth.ts`).
- **Prop Management:**
  - **Interface:** You **MUST** define an interface named `ComponentProps` and **EXPORT** it.
  - **Decoupling:** Define props based on the UI role (e.g., `title`, `description`) rather than the backend entity (e.g., `product_meta_title`).
- **Memoization:** - Wrap expensive sub-components in `React.memo()`.
  - Use `useCallback` for functions passed as props to memoized children.
  - Use `useMemo` for heavy data transformations.
- **Fragments:** Use `<> </>` instead of unnecessary `<div>` wrappers.

## 🧪 2. Testing (Vitest + React Testing Library)
- **Persona:** Senior SDET. Focus on **Behavioral Testing**.
- **Philosophy:** Test what the user sees, not the implementation details. Do not test internal component state.
- **Selectors:** - **Priority 1:** `screen.getByRole()` (e.g., `button`, `heading`). This enforces accessibility.
  - **Priority 2:** `screen.getByLabelText()` or `screen.getByPlaceholderText()`.
  - **Priority 3:** `data-testid` (only for elements with no semantic meaning).
- **Event Simulation:** You **MUST** use `@testing-library/user-event`. Do not use `fireEvent`.
- **Async Handling:** - Use `await screen.findBy...` for elements appearing after a delay.
  - Use `await waitFor()` for assertions that don't have a direct "Find" query.
- **Mocking & Hoisting:** - Use `vi.mock()` with `vi.hoisted()` for external modules or hooks.
  - Always verify `.toHaveBeenCalledTimes(n)`.
- **Strictness:**
  - Use `toStrictEqual()` for object/array assertions.
  - Reset mocks in `afterEach`; clear all mocks and timers in `afterAll`.

## ⚡ 3. Performance & State
- **State Location:** Keep state as close to where it's used as possible. Avoid global state for UI-only toggles.
- **Zustand/Context:** For global state, use Zustand (preferred) or React Context. If using Context, split providers to prevent unnecessary re-renders.
