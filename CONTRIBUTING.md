# 🤝 Contributing to Promps

Thank you for helping improve these AI standards! To maintain the "Staff Engineer" quality of the generated code, please follow these guidelines.

## 📝 Adding a New Framework
If you want to add a new framework (e.g., Svelte, Angular, FastAPI):
1. **Create a new file:** Follow the naming convention `[framework]-rules.md`.
2. **Persona-First:** Ensure the file starts with a high-authority persona (e.g., "You are a Staff Svelte Architect").
3. **Strict Testing:** Include a section on Vitest/Testing library specifics (Selectors, Mocks, Cleanup).
4. **Update Manifest:** Add the new file path to `prompts.json` under `rulesets.frameworks`.

## 💅 Code Style in Prompts
- **Imperative Mood:** Use commands ("Do this," "Never use that") rather than suggestions ("You should...").
- **No Abbreviations:** Use full terms (e.g., "Navigation" instead of "Nav").
- **Accessibility:** All UI rules must include a mention of ARIA labels or semantic HTML.

## ✅ Pull Request Process
- Ensure the rules don't contradict `design-system.md`.
- Test the prompt with an AI agent to ensure it doesn't "hallucinate" or skip the strict testing rules.
