# Repo Orientation

## Quick orientation


Implementation of [shadcn/ui](https://ui.shadcn.com/) components using Vue 3 and [Ark UI](https://ark-ui.com/).
This repository is a Bun-powered monorepo containing `apps/` and `packages/` workspaces.
Use `bun` for installs and running scripts.

## Big picture and structure

- Multi-app monorepo layout (bun workspaces):
  - `apps/` (e.g. `apps/storybook`)
  - `packages/` (e.g. `packages/registry`)

```text
.
├── README.md
├── apps
│   ├── storybook      # Component development and visual testing (Storybook 10 + Vue3 + Vite)
│   └── web            # Documentation site (Astro + Starlight)
├── package.json
├── packages
│   ├── cli            # CLI tool for component installation
│   └── registry       # Core component library (main package)
├── scripts
├── templates
│   └── starter        # Project starter templates
├── .bun-version       # Bun version file
├── package.json       # Root package.json for shared dependencies and scripts
└── tsconfig.json
```

## Developer workflows

Need to `cd` into the specific app or package to run scripts.

- Install dependencies:

  ```bash
  bun install
  ```

- Build the registry package (package-local script):

  ```bash
  cd packages/registry
  bun run registry:build
  ```

Common scripts:

bun run start                 # start an app (if applicable)
bun run dev                   # start development server
bun run build                 # build
bun run lint                  # lint
bun run format [..files]      # fix lint issues
bun run typecheck             # TypeScript type checking
bun run test                  # run tests (vitest)
bun run test:watch            # watch mode

Prefer to inspect each package's own `package.json` for workspace-specific scripts.

## Patterns and conventions

### Registry Package (`packages/registry`)

Components live in `src/components/ui/<name>/`. Each component folder contains:

- `<Name>.vue` — main component using `<script setup>`
- `types.ts` — props interface
- `variant.ts` — CVA variants (size, variant, etc.)
- `_registry.ts` — metadata for the shadcn CLI (`registryItem`)
- `index.ts` — re-exports

Key patterns:
- Headless behavior from **Ark UI** (built on Zag.js state machines)
- Styling via **Tailwind CSS v4** + **class-variance-authority (CVA)**
- `cn()` utility from `lib/utils.ts` (clsx + tailwind-merge)
- `useForwardPropsEmits`, `useForwardProps`, `reactiveOmit` from VueUse for prop forwarding
- `asChild` prop pattern for rendering as a custom element

Global styles and theming are in `src/styles/global.css` (24 color themes, OKLch color space, dark mode via `.dark` class).

### Storybook App (`apps/storybook`)

Stories live in `stories/ui/<name>/`. Each component folder has:
- `<Name>.stories.ts` — story meta, argTypes, and named story exports
- `*Story.vue` — individual story variant components

The `@` alias in storybook Vite config points to `packages/registry/src`.
