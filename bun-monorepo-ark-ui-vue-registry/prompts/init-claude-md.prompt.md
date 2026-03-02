---
agent: agent
---

# Initialize CLAUDE.md

You are a principal engineer documenting a production-grade monorepo for internal
and external stakeholders. Analyze the project and create a tailored `CLAUDE.md`
file at the project root.

## Output Requirements

- **Technically precise**: Name tools, versions, file paths, and commands exactly.
- **Action-oriented**: Every section must answer What, Why, and How for developers
  consuming or contributing to the project.
- **Structured for scannability**: Use headers, bullet points, and code blocks.
  No markdown tables or emojis.
- **Assumption-aware**: If context is missing, state the missing input explicitly
  instead of guessing.

Assume the audience is a senior full-stack engineer evaluating whether to adopt
or contribute to this project.

## Required Sections

1. **Project Overview**
   - One-sentence mission statement
   - Core stack (runtime, framework, UI lib, styling, tooling)
   - Architecture pattern (e.g., monorepo with workspaces)

2. **Project Structure**
   - Tree diagram of top-level directories with 1-line purpose per directory
   - Call out non-obvious decisions (e.g., why `scripts/` is separate from
     `packages/`)

3. **Key Features**
   - List only differentiating capabilities, not generic traits like
     "uses TypeScript"
   - Prioritize: accessibility, extensibility, DX, maintainability

4. **Building and Running**
   - Prerequisites (exact runtime/tool versions)
   - Commands grouped by: setup, dev, build, test, lint/format
   - Include port numbers, entry points, and failure symptoms
     (e.g., "If bun dev fails with X, check Y")

5. **Development Conventions**
   - Code style enforcement (linter, formatter, pre-commit hooks)
   - Commit policy
   - Testing strategy (unit, e2e, visual regression)
   - Type safety boundaries (strict mode? isolatedModules?)

6. **Key Dependencies**
   - Only list non-default or opinionated choices
   - For each: explain why it was chosen over alternatives
     (e.g., "Ark UI over Radix Vue for framework-agnostic composables")

7. **Configuration Files**
   - Map config files to their scope
     (e.g., `tsconfig.json` → monorepo root, project references enabled)
   - Highlight non-standard settings that affect behavior

8. **Project Context**
   - Explain the problem being solved and gap this project fills
   - Compare to alternatives
     (e.g., "Unlike shadcn/ui, this targets Vue 3 + Ark, not React + Radix")
   - State explicit non-goals

## Notes

- Never say "This project is great" or similar. Be neutral and precise.
- Do not hallucinate APIs. Use context7 to gather information if needed.
- If uncertain, state assumptions explicitly.
