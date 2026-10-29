Update Refraction documentation to reflect recent code changes. Code is authoritative — the docs follow.

## Steps

1. Run `git diff HEAD~1 HEAD --name-only` (or `git diff --staged --name-only` if reviewing staged changes) to see what changed.

2. For each changed file, determine which Refraction doc(s) are affected:
   - Changes to system boundaries or external integrations → update `docs/system.md`
   - Changes to a container's interfaces, technology, or responsibilities → update `docs/containers/[name].md`
   - Changes to a component's behavior, interfaces, or code pointers → update `docs/components/[name].md`
   - Changes to behavior detailed enough for a shared spec (algorithms, protocols, interaction models) → update `docs/specs/[name].md`
   - Changes to build, release, deploy, install, or runtime concerns → update `docs/ops/[name].md`
   - Changes to how an external system is called, or to its constraints and limits → update `docs/external/[name].md`

3. Read the current content of each affected doc before editing it.

4. Update only what changed. Do not rewrite sections that are still accurate.

5. If a change introduces a new component or container that is not documented yet, create the missing file following the Refraction standard (https://signalshell.com/refraction/v1.2).

6. If a change removes a component or container, remove or archive its doc file.

## Rules

- No diagrams of any kind. Not ASCII art, not Mermaid, not PlantUML. Prose, lists, and tables only.
- Level markers must be present at the top of each file (`<!-- L1: System Context -->`, `<!-- L2: Container -->`, `<!-- L3: Component -->`, `<!-- L4: Spec -->`, `<!-- Ops -->`, `<!-- External -->`).
- Code pointers in L3 files must be kept current — update file paths and function names if they moved.
- Do not update docs for files you do not understand. Flag uncertain changes for human review instead.

## After updating

Report which doc files were changed and why. Flag any changes where you were uncertain whether the doc update is correct.
