# 🛠 API & Global Testing Rules

## 🌐 API Communication
- **Interceptors:** Use Axios/Fetch interceptors for Auth headers and 401 handling.
- **Resilience:** Every request MUST have a **10,000ms** timeout.

## 🧪 Global Test "Strict Mode"
- **Descriptions:** All tests must start with the word **"should"**.
- **Mocking:** Use `vi.hoisted()` for `vi.fn()` inside `vi.mock()`.
- **Assertions:**
  - Always verify `.toHaveBeenCalledTimes()`.
  - Use `toStrictEqual()` for objects/arrays.
- **Cleanup:** Reset mocks in `afterEach`; clear all mocks and timers in `afterAll`.
