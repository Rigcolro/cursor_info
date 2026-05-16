---
name: scrm-chat-desktop
description: Project-specific development rules for the scrm_chat_desktop Electron + Vue application. Use when working in E:\zlketang\scrm_chat_desktop or when the user asks Codex to follow that project's existing Cursor rules, Vue conventions, API patterns, store conventions, packaging constraints, or resource URL rules.
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
user-invocable: true
---

# scrm-chat-desktop

Use this skill when editing, reviewing, or planning work for the `scrm_chat_desktop` project.

## Workflow

1. Read `references/project-core.mdc` first and treat it as the project-wide rule source.
2. Read additional rule files only when the task touches that area:
   - `references/vue-component.mdc` for Vue SFC work
   - `references/api-call.mdc` for `src/renderer/src/api/modules/*`
   - `references/pinia-store.mdc` for `src/renderer/src/stores/*`
   - `references/tyscript-style.mdc` for TypeScript handling conventions
   - `references/interface-convention.mdc` for UI layout conventions such as `el-scrollbar`
   - `references/packaging.mdc` for build, packaging, `package.json`, `electron.vite.config.ts`, `electron-builder.yml`, or `scripts/build.mjs`
3. Keep edits minimal and aligned with the existing repository style.
4. If the project rule conflicts with an explicit user request, follow the user's request and call out the conflict briefly.

## Important local conventions

- Respect the project's Electron, Vue 3, TypeScript, Element Plus, Tailwind, and pnpm setup.
- Use IPC through the project's declared channel and preload registration flow.
- Avoid protocol-relative external resource URLs unless they are passed into the project's resource normalization helper.
- Prefer the project's existing API wrapper, store patterns, and global utility conventions.

## Notes

- The original source of truth for these rules is the project's `.cursor/rules` directory.
- The copied `.mdc` files in this skill exist so Codex can follow the same rules without modifying the repository.
