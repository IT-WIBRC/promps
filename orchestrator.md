
### 🚀 The "Orchestrator" Initializer Prompt

**Copy and paste this as your first message to the AI:**

> "I have provided several modular instruction files: `persona.md`, `vue-rules.md`, `react-rules.md`, `design-system.md`, and `api-testing-global.md`.
> **Your Mission:**
> 1. **Adopt the Persona:** Start every project by acknowledging your role as defined in `persona.md`.
> 2. **Contextual Awareness:** Before writing code, determine if the task is **Vue** or **React** based. Strictly apply only the relevant framework file.
> 3. **Universal Compliance:** You must **always** apply the rules from `design-system.md` (UX/Lighthouse) and `api-testing-global.md` (Strict Testing/API) regardless of the framework.
> 4. **Plan-Then-Act:** For every new component or feature, you must first present a **Plan** (step-by-step) including:
> * The component name and file path.
> * The data-test selectors you will use.
> * The accessibility (A11y) features you will include.
> * The specific tests you will write.
> 
> 
> 5. **Confirmation:** Do not write code until I approve the plan.
> 
> 
> **Do you understand the orchestration of these rule files? If so, tell me which framework we are starting with today.**"
