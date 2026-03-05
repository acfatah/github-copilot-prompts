# Coding Style

- Always fix lint errors as the last task, after all other tasks.
- Use `bun format` or `bun format:changed` to auto-fix formatting.
- ESLint uses `@acfatah/eslint-preset` via `eslint.config.ts`.

Important rules:

- Two-space indent, spaces NEVER use tabs.
- Single quotes.
- Alphabetized imports by file name with
  `perfectionist/sort-imports`.
- Empty line before `return`.
- Top-level functions should use `function` declarations.

Vue conventions:

- Components use `<script setup lang="ts">` exclusively.
- Use `cn()` from `src/lib/utils.ts` for conditional class merging.
