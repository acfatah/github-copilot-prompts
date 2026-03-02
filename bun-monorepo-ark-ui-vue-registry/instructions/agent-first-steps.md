# Agent First Steps

When editing this repository:

1. Read `package.json`, `tsconfig.json`, and `README.md` at repo root.
2. Inspect `packages/<package>/package.json` for package-local scripts and
   dependencies.
3. If TypeScript changes are needed, prefer minimal `extends`-based overrides in
   package `tsconfig.json` instead of changing root compiler flags without clear
   requirement.
4. If a change touches workspace resolution or workspaces, verify and correct
   `workspace` globs in root `package.json`.
