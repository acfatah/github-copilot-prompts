# Coding Style

- Always fix lint errors as the last task, after all other tasks.
- Use `bun run format [..file]` to format code or files.
- ESLint uses `@antfu/eslint-config` via `eslint.config.ts`.

Important rules:

- Use spaces instead of tabs.
- Two-space indent.
- Single quotes.
- Alphabetized imports by file name with
  `perfectionist/sort-imports`.
- Empty line before `return`.
- Top-level functions should use `function` declarations.

Naming conventions:

- React/Redux slices use PascalCase.
- Hooks/helpers/files use camelCase.
- Config keys use UPPER_SNAKE_CASE.
