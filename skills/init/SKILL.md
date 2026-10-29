---
description: Initialize Refraction documentation for a project from scratch. Use when a project has no docs/ directory or when starting Refraction from the beginning.
---

Initialize Refraction documentation for this project.

Read the codebase to understand its structure, then create a complete set of Refraction docs following the Refraction documentation standard v1.2 (https://signalshell.com/refraction/v1.2).

## Steps

1. Explore the project.
   Read README, DEVELOPMENT.md, and main source files to learn what the system does, its deployable units, its components, and the external systems it talks to.

2. Create `docs/system.md` (L1) and start it with `<!-- L1: System Context -->`.
   Put this citation line near the top:
   Documentation follows the [Refraction documentation standard v1.2](https://signalshell.com/refraction/v1.2).
   Include what the system does, external actors (users, systems, integrations), a container index with one-line descriptions and links, and constraints and non-goals.
   Link to every container.

3. Create `docs/containers/[name].md` (L2) for each separately deployable or runnable unit, starting with `<!-- L2: Container -->`.
   Put shared infrastructure in `containers/platform.md`.
   Include responsibility, technology, every external interface with direction, a component index with links, and key decisions.
   Link to files in `docs/external/` where there is real API surface.

4. Create `docs/components/[name].md` (L3) for each meaningful component, starting with `<!-- L3: Component -->`.
   Keep files flat in `docs/components/`.
   Include role, interfaces (inputs, outputs, events), constraints and decisions, and code pointers: exact file paths and function names.

5. Create `docs/specs/[name].md` (L4) for behaviors too detailed for their component or shared by several components, starting with `<!-- L4: Spec -->`.
   Specs are shared, not owned: link to them from every affected component.

6. Create `docs/ops/[name].md` for each applicable operational concern, starting with `<!-- Ops -->`.
   Common types: build, release, deploy, install, runtime.
   Create only the files that apply and name them freely.

7. Create `docs/external/[name].md` for each external system with significant API surface, starting with `<!-- External -->`.
   Document what the system is, the specific calls and patterns you use, constraints and limits, and a link to official docs.
   Passing references don't need a file.

## Rules

- No hand-maintained diagrams: not Mermaid, not PlantUML, not ASCII art.
  Images are allowed as a supplement: each is dated, says what it shows, and every fact it shows is also written in the text.
- One fact, one place: write each fact once, in the file at the lowest layer that owns it; higher layers state it in at most one sentence and link to that file.
- Constants: name a constant together with the file that defines it, for example `relayMaxPerChan` in `relay.go`, and write its value next to the name where the reader needs it.
- Code pointers are a general principle, most natural at L3 and L4: file paths and module names let readers navigate from a doc straight to the implementation.
- Describe the system as it is.
  History lives in version control; do not write accounts of how something used to work.
- One sentence per line.
  Split a line clearly longer than about 200 characters at a natural break; if there is none, leave it long.
  Do not break at every comma.
- Every file must be reachable from `docs/system.md` by following links; no orphan files.
- Granularity: a component is something you'd explain separately when onboarding a new developer.

## After creating the files

Report which files were created and flag anything you were uncertain about (fuzzy container/component boundaries, missing context about external systems, etc.).
