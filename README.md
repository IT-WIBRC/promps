# 🤖 AI Framework Prompts (promps)

A modular library of high-authority Markdown configuration files designed to govern AI agents (like Cursor, GitHub Copilot, or GPT-4). This repository ensures that generated code adheres to strict architectural standards, performance benchmarks (Lighthouse 100), and specific framework philosophies.

## 📁 Repository Structure

| File | Description |
| :--- | :--- |
| **`orchestrator.md`** | The master prompt to initialize an AI session and link all rules. |
| **`persona.md`** | Defines the "Staff Engineer" persona and authority level. |
| **`vue-rules.md`** | Vue 3 Composition API standards (including AlexOp patterns). |
| **`react-rules.md`** | React 18+ standards for hooks, performance, and RTL testing. |
| **`design-system.md`** | UI/UX guidelines (8pt grid, A11y, Dark Mode, Lighthouse). |
| **`api-testing-global.md`** | Rules for Axios/Fetch, Vitest, and strict test assertions. |

---

## 🚀 How to Use

### Option 1: Manual Initialization (Recommended)
When starting a new conversation with an AI agent, copy the contents of `orchestrator.md` and paste it as your first message. The AI will then ask for the relevant framework files based on your project.

### Option 2: Cursor / Copilot Custom Rules
If you use **Cursor**, you can copy the contents of these files into your `.cursorrules` file or reference this repository folder to provide constant context to the IDE.

---

## 🛠 Core Principles

### 1. Zero-Tolerance Testing
- **Strict Mocking:** Mandatory use of `vi.hoisted()` and `toHaveBeenCalledTimes()`.
- **Isolation:** Components are treated as black boxes; sub-components are always stubbed.

### 2. Design Excellence
- **Lighthouse 100:** All generated components must prioritize semantic HTML, image optimization, and accessibility.
- **A11y:** Mandatory `aria-label` for icon buttons and strict color contrast ratios.

### 3. Architecture
- **Domain Agnostic:** Props are defined by UI role, not backend entities.
- **Logic Extraction:** Complex logic must live in Composables (Vue) or Custom Hooks (React).

---

## 📜 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
