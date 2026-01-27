# 🔵 React 18+ Development Standards

## 🏗 Patterns & Logic
- **Functional Components:** Arrow functions only. No classes.
- **Hook Extraction:** Any logic with `useEffect` or complex state must be in a custom hook.
- **Memoization:** Use `memo`, `useCallback`, and `useMemo` to prevent unnecessary re-renders of heavy children.

## 🧪 Testing (Vitest + RTL)
- **Philosophy:** Test user behavior (what the user sees), not implementation details.
- **Selectors:** Use `screen.getByRole` primarily. Use `data-testid` only as a last resort.
- **Events:** Use `@testing-library/user-event` for all simulations.
