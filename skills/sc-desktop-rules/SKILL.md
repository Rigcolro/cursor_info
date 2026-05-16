---
name: sc-desktop-rules
description: Project rules for the scrm_chat_desktop codebase. Use when working in E:\zlketang\scrm_chat_desktop, or when the user asks to follow that project's existing Cursor rules, Vue conventions, API module patterns, Pinia store patterns, packaging constraints, or resource URL rules.
---

# sc-desktop-rules

Use this skill for work in the `scrm_chat_desktop` project.

## Workflow

1. Read `references/project-core.mdc` first.
2. Read only the rule files needed for the current task:
   - `references/vue-component.mdc`
   - `references/api-call.mdc`
   - `references/pinia-store.mdc`
   - `references/tyscript-style.mdc`
   - `references/interface-convention.mdc`
   - `references/packaging.mdc`
3. Treat those `.mdc` files as high-priority local project rules.
4. Keep edits minimal and consistent with the repository style.
5. If a project rule conflicts with an explicit user request, follow the user request and note the conflict briefly.

## Important conventions

- Respect the existing Electron, Vue 3, TypeScript, Element Plus, Tailwind, and pnpm setup.
- Follow the project's IPC channel, preload, and registration flow.
- Avoid protocol-relative external resource URLs unless they go through the project's resource normalization helper.
- Prefer the project's existing API wrapper, store conventions, and shared utilities.

## References

The copied rule files mirror the project's `.cursor/rules` directory so Codex can follow the same constraints without modifying the repository.