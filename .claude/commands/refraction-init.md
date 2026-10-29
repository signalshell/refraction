Initialize Refraction documentation for this project.

Read the codebase to understand its structure, then create a complete set of Refraction docs following this standard: https://signalshell.com/refraction/v1.2

## Steps

1. Explore the project: read README, DEVELOPMENT.md, main source files. Understand what the system does, its major components, and how they interact.

2. Create `docs/system.md` (L1). Start with `<!-- L1: System Context -->`. Include:
   - What the system does and why it exists (one paragraph)
   - External actors: users, systems, integrations it talks to (bullet list)
   - Container index with one-line descriptions and links (e.g. `- [name](containers/name.md) — what it does`)
   - Constraints and non-goals

3. Create `docs/containers/[name].md` for each deployable unit (L2). Start with `<!-- L2: Container -->`. Include:
   - Responsibility (one paragraph)
   - Technology: language, runtime, binary location
   - Interfaces: every external interface with direction (HTTP, file system, CLI, etc.)
   - Component index with links
   - Key decisions: non-obvious architectural choices

4. Create `docs/components/[name].md` for each meaningful component (L3). Start with `<!-- L3: Component -->`. Include:
   - Role (one paragraph)
   - Interfaces: inputs, outputs, events
   - Code pointers: exact file paths and function names
   - Constraints and decisions

5. Create `docs/specs/[name].md` (L4) for any behavioral or algorithm specs worth documenting separately: algorithms, protocols, interaction models. Specs are shared, not owned — link to them from every affected component.

6. Create `docs/ops/[name].md` (`<!-- Ops -->`) for applicable operational concerns: build, release, deploy, install, runtime.

7. Create `docs/external/[name].md` (`<!-- External -->`) for each external system with significant API surface. Passing references don't need a file.

## Rules

- No diagrams of any kind. Not ASCII art, not Mermaid, not PlantUML. Prose, lists, and tables only.
- Every container in system.md must have a corresponding file. Every component in a container file must have a corresponding file.
- Code pointers are a general principle, most natural at L3 and L4 — they bridge doc to implementation.
- Components are flat in `docs/components/` unless two containers have components with the same name.
- Granularity: if you'd explain it separately when onboarding a new developer, it's a component. Otherwise, mention it in the container doc.

## After creating the files

Report which files were created and flag anything you were uncertain about (fuzzy container/component boundaries, missing context about external systems, etc.).
