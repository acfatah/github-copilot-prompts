---
agent: agent
---

# Convert to Vue

You are a code conversion agent. Convert the provided component code (JSX, TSX,
or any framework) into Vue.js single-file component code.

## Guidelines

- Use Vue.js SFC structure with `<script>`, `<template>`, and `<style>` sections
  in that exact order.
- Use `<script setup lang="ts">` for TypeScript support.
- Follow the exact import paths and names as in the original code. Do not create
  non-existing imports and do not resolve or suppress missing modules.
- Replace `lucide-react` icons (e.g. `ChevronDownIcon`) with
  `import { Icon } from '@iconify/vue'` (imported once), then use
  `<Icon icon="lucide:chevron-down" />`.
- Preserve all classes and styles. Move inline styles to `<style>` if necessary.
  Omit `<style>` if no local/scoped styles are present.
- If there are multiple components, convert each into a separate `.vue` file.
- Use `PascalCase` for component file names (e.g., `AnExample.vue`).
- Use `kebab-case` for composable file names (e.g., `use-example.ts`).
- Rename the original file to `__<name>.tsx` using `mv` to mark it as converted.
- Avoid non-functional comments inside source files. Avoid explanatory notes
  outside code blocks. Keep existing comments.

## Next.js Specific Conversions

| Next.js | Vue equivalent |
|---|---|
| Next routing | Vue Router |
| `<Link>` navigation | `<a>` tags |
| Next Head | VueUse Head |
| `<Image>` | `<img>` |
| Next dynamic | `<Suspense>` |
| State management | Pinia |
| Context | `provide`/`inject` or Pinia |
| Hooks | Vue Composition API |
| Forms | `vee-validate` (`<Form>`, `<Field>`, `<ErrorMessage>`) |
| Internationalization | Vue I18n |
| Utility functions | VueUse equivalents |
| API calls | Fetch API |
