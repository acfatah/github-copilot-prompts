# Testing and Verification

- Run `bun test` to execute tests (Vitest).
- Run `bun typecheck` to verify TypeScript types (`vue-tsc --noEmit`).
- Run `bun run build` for full type-check + production build.
- Start with specific tests near changed code, then broaden.
- Do not fix unrelated broken tests.
