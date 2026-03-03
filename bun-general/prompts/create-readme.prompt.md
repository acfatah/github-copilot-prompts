---
agent: agent
description: Prompt to create a comprehensive README file for a project.
---

## Objective

Generate a comprehensive `README.md` for the current project by analyzing its codebase, configuration files, and project structure.

## Step 1: Explore the Project

Read and analyze the following to understand the project:

- `package.json` (or equivalent manifest) — name, description, scripts, dependencies, devDependencies
- Runtime version files (e.g., `.node-version`, `.bun-version`, `.nvmrc`, `.tool-versions`)
- Build/bundler config (e.g., `vite.config.ts`, `webpack.config.js`, `next.config.js`)
- TypeScript config (`tsconfig.json` and any project references)
- Linter/formatter config (e.g., `eslint.config.ts`, `.prettierrc`)
- Git hooks config (e.g., `.husky/`, `simple-git-hooks` in `package.json`)
- Commit lint config (e.g., `commitlint.config.ts`)
- Environment variable files (`.env.example`, `.env.local.example`)
- Source directory structure (`src/` or equivalent)
- Existing documentation files (`CLAUDE.md`, `CONTRIBUTING.md`, etc.)

## Step 2: Generate the README

Write `README.md` with the following sections. Adapt each section to what actually exists in the project — omit sections that don't apply, and add sections for notable features not listed here.

### Section Structure

#### 1. Header

- Project name as H1
- One-line tagline as blockquote
- Short paragraph describing what the project does

#### 2. Project Overview

- Bullet list of 3–5 key technologies used, each with a brief description

#### 3. Tech Stack

- Markdown table with columns: **Category** | **Technology**
- Cover all relevant categories: runtime, framework, language, UI components, styling, routing, state management, utilities, icons, fonts, build tool, linting, testing, commit hooks, etc.
- Include specific version numbers where they matter (e.g., "Vue.js 3.5+", "Tailwind CSS v4")

#### 4. Architecture

- Describe the project structure using a list of top-level directories
- Each entry: directory path followed by a colon and brief description
- Focus on `src/` subdirectories and their purpose

#### 5. Building and Running

- **Prerequisites**: runtime requirements with version info
- **Commands table**: Markdown table with columns **Command** | **Description** — list all scripts from the manifest
- **Git Hooks**: describe any pre-commit, commit-msg, or other hooks

#### 6. Development Conventions

- Bullet list covering: code style, styling approach, component syntax, accessibility, file structure conventions

#### 7. Key Dependencies

- Bullet list of notable production dependencies with short descriptions

#### 8. Configuration Files

- Bullet list of config files with their purpose

#### 9. Project Features (detailed subsections)

Create H3 subsections for each major feature area. Common subsections include:

- **Code Style**: linter setup, formatting rules, plugin details
- **Framework Conventions**: component syntax, path aliases, layout system
- **TypeScript**: strict mode, project references, path aliases
- **Styling**: CSS framework setup, theme configuration, utility functions
- **Component Patterns**: code example showing the standard component template
- **Router Patterns**: route definition style, meta properties, loading indicators
- **Internationalization**: i18n setup, message files, how to add a new locale
- **API / Data Fetching**: HTTP client setup, auth headers, base URL config

Include code examples (fenced code blocks) where they clarify usage patterns.

#### 10. Key Utilities

- Notable utility functions with import path and brief usage example in a code block

#### 11. Commit Conventions

- Commit message format template
- List of valid types with examples

#### 12. Environment Variables

- Markdown table with columns: **Variable** | **Description**
- Note any security considerations (e.g., client-side exposure of `VITE_` prefixed vars)

#### 13. Notes

- Any important caveats, gotchas, or project-specific information that doesn't fit elsewhere

## Guidelines

- Use clear, concise language
- Prefer tables for structured data (tech stack, commands, env vars)
- Prefer bullet lists for descriptive lists
- Include code examples only where they genuinely clarify patterns
- Use accurate version numbers from the actual config files
- Do not invent features or dependencies — only document what exists
- Keep the tone professional and direct
