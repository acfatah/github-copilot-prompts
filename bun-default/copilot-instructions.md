## Quick orientation

This repository uses bun as the runtime. Use `bun` command for installs and running
scripts.

## Big picture and structure

```
.
├── README.md
├── eslint.config.ts
├── package.json
├── scripts
├── src
├── tests
└── tsconfig.json
```

## Developer workflows (commands & conventions)

To install dependencies, use `bun install` command.

Common scripts are:
  - `bun run start` - start the app (if applicable)
  - `bun run dev` - start development server (if applicable)
  - `bun run build` - build the app (if applicable)
  - `bun run preview` - preview the built app (if applicable)
  - `bun run lint` - lint the codebase (if applicable)
  - `bun run typecheck` - run type checking (if applicable)
  - `bun run format` - fix lint issues (if applicable)
  - `bun run test` - run tests (if applicable)

## Coding Style

- Always fix lint errors as the last task, only after all other tasks are completed.
- Use `bun run format [..file]` to format code or files.
- We are using ESLint with `@antfu/eslint-config` rules via `eslint.config.ts`.
  The following is the summary of important rules:
  - use spaces for indentation
  - two-space indent
  - single quotes
  - alphabetised imports (file name) with `perfectionist/sort-imports`
  - empty line before `return`
  - top-level functions should be declared with function keyword

## Testing & Verification

- Do not merge Bun.env and process.env. Run commands from root directory.
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
- Optionally add scope if applicable. E.g. `fix(user-login):`, `feat(web):`
- Limit subject line to 60 characters.
- Use the body to explain what and why, not how.
- Use bullets in the body if multiple points.

## Response & Output Style

- Be concise; prioritize actionable guidance.
- Use what, why, and how to explain concepts.
- Include tips, gotchas, and common pitfalls; something that need to be aware of.
- Use bullets and short sections for scanability.
- Use tables whenever helpful.
- Use markdown formatting for code snippets and commands.
- Wrap commands, file paths, env vars, and code identifiers in backticks.
- Provide bash-ready commands in fenced blocks when giving steps.
- When editing code, prefer minimal diffs and preserve existing style.
- If you create multiple files or non-trivial code, include a short run/test snippet.
- Never use emojis unless explicitly asked and avoid en or em dashes.
