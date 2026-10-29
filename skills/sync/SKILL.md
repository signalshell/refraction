---
description: Update Refraction documentation to reflect recent code changes. Code is authoritative. Use after modifying source files, adding features, changing interfaces, or restructuring components.
---

Update Refraction documentation to reflect recent code changes.
Code is authoritative — the docs follow.

## Steps

1. Run `git diff HEAD~1 HEAD --name-only` (or `git diff --staged --name-only` if reviewing staged changes) to see what changed.

2. For each changed file, determine which Refraction doc(s) are affected:
   - Changes to system boundaries, external actors, or non-goals → update `docs/system.md`
   - Changes to a container's interfaces, technology, or responsibilities → update `docs/containers/[name].md`
   - Changes to a component's behavior, interfaces, or code pointers → update `docs/components/[name].md`
   - Changes to behavior detailed enough for a shared spec (algorithms, protocols, interaction models) → update `docs/specs/[name].md`
   - Changes to build, release, deploy, install, or runtime concerns → update `docs/ops/[name].md`
   - Changes to how an external system is called, or to its constraints and limits → update `docs/external/[name].md`

3. Read the current content of each affected doc before editing it.

4. Update only what changed; do not rewrite sections that are still accurate.

5. Apply the v1.2 rules while editing: one sentence per line, describe the current state, and keep every fact in the single file that owns it.
   Do not copy a fact into a second file; link instead.

6. If a change introduces a new container, component, spec, ops concern, or external system with no doc yet, create the missing file following the Refraction documentation standard v1.2 (https://signalshell.com/refraction/v1.2).

7. If a change removes a component, container, spec, ops file, or external system, delete its doc and fix every link that pointed to it.

## Rules

- No hand-maintained diagrams: not Mermaid, not PlantUML, not ASCII art.
  Images are allowed as a supplement: dated, saying what they show, with every shown fact also written in the text.
- Every doc file keeps its marker at the top: `<!-- L1: System Context -->`, `<!-- L2: Container -->`, `<!-- L3: Component -->`, `<!-- L4: Spec -->`, `<!-- Ops -->`, `<!-- External -->`.
- Code pointers are a general principle, most natural at L3 and L4: keep file paths and function names current when they move.
- If the code changed a named constant's value, update the value written next to the constant in the docs.
- Keep every file reachable from `docs/system.md`; fix links when removing or renaming files.
- Do not update docs for files you do not understand; flag uncertain changes for human review instead.

## After updating

Report which doc files were changed and why.
Flag any changes where you were uncertain whether the doc update is correct.
