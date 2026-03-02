# Repo Orientation

## Quick orientation

This repository is a Bun-powered monorepo containing `apps/` and `packages/`.
Use `bun` for installs and running scripts.

## Big picture and structure

- Multi-app monorepo layout:
  - `apps/` (e.g. `apps/storybook`)
  - `packages/` (e.g. `packages/registry`)

```text
.
├── README.md
├── apps
│   ├── storybook      # Storybook app for component development and visual testing
│   └── web            # Main landing page app built with Astro
├── package.json
├── packages
│   └── registry       # The component registry
├── scripts
├── templates
│   └── starter        # Template for starting new projects
└── tsconfig.json
```

## Developer workflows

Need to `cd` into the specific app or package to run scripts.

- Install dependencies (root):

  ```bash
  bun install
  ```

- Build the registry package (package-local script):

  ```bash
  cd packages/registry
  bun run registry:build
  ```

Common scripts:

- `bun run start` (if applicable)
- `bun run dev` (if applicable)
- `bun run build` (if applicable)
- `bun run preview` (if applicable)
- `bun run lint` (if applicable)
- `bun run typecheck` (if applicable)
- `bun run format` (if applicable)
- `bun run test` (if applicable)

Prefer to inspect each package's own `package.json` for package-specific scripts.
