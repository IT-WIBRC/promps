# 🟢 Vue.js 3 Development Standards

## 🏗 Architecture & Logic
- **Reactivity:** Use `<script setup>` and Composition API exclusively.
- **Composables:** One responsibility per composable. Return objects (e.g., `return { state, action }`).
- **Context Safety:** If using `inject`, throw a descriptive error if the provider is missing.
- **Dumb Templates:** Move all logic into `computed()` properties.

## 🧱 Component Rules
- **Naming:** Layout/Single-instance components MUST start with `The` (e.g., `TheNavbar.vue`).
- **Props:** Define and **EXPORT** a `Props` interface. Use UI-centric names (e.g., `title`) not domain names (e.g., `userEmail`).

## 🧪 Testing (Vitest + @vue/test-utils)
- **Isolation:** Always `shallowMount` or stub child components (Black Box testing).
- **Routing:** Use `RouterLinkStub`. Explicitly assert the `to` prop object.
- **Composables:** Use a `withSetup` wrapper for tests involving lifecycle hooks.
