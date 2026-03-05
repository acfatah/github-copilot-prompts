# Repo Orientation

## Commands

```bash
bun install          # Install dependencies (use Bun, not npm/yarn)
bun dev              # Start dev server at localhost:5173
bun run build        # Type-check + build for production
bun typecheck        # Run vue-tsc --noEmit
bun lint             # ESLint on all files
bun lint:changed     # ESLint on changed files only
bun format           # Auto-fix formatting via ESLint
bun format:changed   # Format changed files only
bun ui               # Manage UI components from registry
```

Always use `bun` (not `npm` or `node`). All scripts use `bunx --bun` to
ensure Bun runtime.

## Architecture

### Routing

Routes are **co-located with their pages**: each feature has a
`src/pages/[feature]/routes.ts` that exports route definitions, which are
then imported into `src/router/index.ts`. Route meta supports:

- `titleKey: RouteTitleKey` - i18n key for localized page title
  (from `routeTitle.*`)
- `title: string` - direct page title
- `layout: Component` - custom layout (defaults to `BlankLayout`)

NProgress loading bar is integrated into the router via `useNProgress()`.

### Layout System

`App.vue` dynamically renders layouts based on `$route.meta.layout`:

```vue
<component :is="$route.meta.layout || BlankLayout" />
```

Built-in layouts: `BlankLayout` (default), `MutedLayout` (muted background).
Add new layouts in `src/layouts/`.

### API / Data Fetching

`src/lib/fetch.ts` wraps VueUse's `createFetch()` with:

- Base URL from `VITE_API_URL`
- `Authorization` header from `localStorage.token`
- `Accept-Language` from current i18n locale
- `credentials: 'include'` for cookie-based auth

### Internationalization

vue-i18n in composition mode (`legacy: false`). Messages in
`src/i18n/messages/[locale].ts`. Type-safe schema in `src/i18n/types.ts`.

To add a new locale:

1. Create `src/i18n/messages/[locale].ts`
2. Register in `src/i18n/index.ts` under `messages` and `SUPPORTED_LOCALES`
3. Add type to `SupportedLocale` in `src/i18n/types.ts`
4. Keep `routeTitle` keys consistent across all locales

### Key Utilities

- `cn()` in `src/lib/utils.ts` - combines `clsx` + `tailwind-merge` for
  conditional class merging
- `@` path alias resolves to `src/`

### Styling

Tailwind CSS v4 via `@tailwindcss/vite`. Global theme in
`src/styles/global.css` using oklch() color space with light/dark mode
(`.dark` class). SVG files can be imported as Vue components via
`vite-svg-loader`.

## Environment Variables

Copy `.env.example` to `.env`:

| Variable          | Description                                             |
| ----------------- | ------------------------------------------------------- |
| `VITE_PAGE_TITLE` | Default browser tab title                               |
| `VITE_API_URL`    | Backend API base URL (default: `http://localhost:3000`) |
| `REGISTRY_URL`    | UI component registry URL                               |

All `VITE_` variables are exposed client-side and included in production
builds.
