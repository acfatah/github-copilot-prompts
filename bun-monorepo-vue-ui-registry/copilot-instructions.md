## Quick orientation

This repository is a bun-powered monorepo containing `apps/` and `packages/`.
Use `bun` for installs and running scripts.

## Big picture and structure

- Multi-app monorepo layout: `apps/` (e.g. `apps/storybook`) and `packages/` (e.g. `packages/registry`).

```
.
├── README.md
├── apps
│   ├── storybook		# Storybook app for component development and visual testing
│   └── web	        # Main landing page app built with Astro
├── package.json
├── packages
│   └── registry   	# The component registry
├── scripts
├── templates
│   └── starter		# Template for starting new projects
└── tsconfig.json
```

## Developer workflows (commands & conventions)

Need to `cd` into the specific app or package to run scripts.

- Install dependencies (root):

  ```bash
  bun install
  ```

- Build the registry package (package-local script):

  ```bash
  cd packages/registry
  bun run registry:build   # runs `shadcn build` as defined in package.json
  ```

Common scripts are:
  - `bun run start` - start the app (if applicable)
  - `bun run dev` - start development server (if applicable)
  - `bun run build` - build the app (if applicable)
  - `bun run preview` - preview the built app (if applicable)
  - `bun run lint` - lint the codebase (if applicable)
  - `bun run typecheck` - run type checking (if applicable)
  - `bun run format` - fix lint issues (if applicable)
  - `bun run test` - run tests (if applicable)

Prefer to inspect a package's own `package.json` for package-specific scripts.

## What an AI agent should do first when editing

1. Read `package.json`, `tsconfig.json`, and `README.md` at the repo root.
2. Inspect `packages/<package>/package.json` for package-local scripts and
   dependencies (example: `packages/registry/package.json`).
3. If TypeScript changes are needed, prefer adding minimal `extends`-based overrides
   in the package `tsconfig.json` rather than editing root compiler flags without requirement.
4. If a change touches workspace resolution or workspaces, verify and correct the
   `workspace` globs in the root `package.json`.

## Coding Style

- Always fix lint errors as the last task, only after all other tasks are completed.
- Use `bun run format [..file]` to format code or files.
- We are using ESLint with `@antfu/eslint-config` rules via `eslint.config.ts`.
  The following is the summary of important rules:
  - two-space indent
  - single quotes
  - alphabetised imports (file name) with `perfectionist/sort-imports`
  - empty line before `return`
  - top-level functions should be declared with function keyword
- Naming React components/Redux
  - slices use PascalCase
  - hooks/helpers/files use camelCase
  - config keys use UPPER_SNAKE_CASE

## Testing & Verification

- Do not merge Bun.env and process.env. Find where dotenv files are located,
  cd into that directory and run commands from there.
- Start with specific tests near changed code, then broaden.
- Don’t fix unrelated broken tests.

## Documentation or Comments

- Limit lines around 80 characters. Insert line breaks with correct indents so line
  stays between 80 characters.
- Be concise, use bullets.
- Use markdown formatting for code snippets and commands.
- Wrap commands, file paths, env vars, and code identifiers in backticks.
- Use tables in documentation whenever helpful.

## Commit Messages

- Use conventional commits: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `style`
- Use the imperative mood ("add", "fix", "change", "remove")
- Always add scope based on workspace except for root. E.g. `fix(registry):`, `feat(web):`
- Use directory names either from `apps/` or `packages/` as scope.
- Limit subject line to 60 characters.
- Use the body to explain what and why, not how.
- Use bullets in the body if multiple points.

## Response & Output Style

- Be concise; prioritize actionable guidance.
- Use what, why, and how to explain concepts.
- Include tips, gotchas, and common pitfalls; something that need to be aware of.
- Use bullets and short sections for scannability.
- Use tables whenever helpful.
- Use markdown formatting for code snippets and commands.
- Wrap commands, file paths, env vars, and code identifiers in backticks.
- Provide bash-ready commands in fenced blocks when giving steps.
- When editing code, prefer minimal diffs and preserve existing style.
- If you create multiple files or non-trivial code, include a short run/test snippet.
- Never use emojis unless explicitly asked and avoid en or em dashes.
