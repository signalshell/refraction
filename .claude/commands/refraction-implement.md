Update code to match Refraction documentation. Docs are authoritative — the code follows.

Use this when you have written or updated docs first and want the implementation to catch up. This is the "docs-first" workflow: specify what you want in the architecture docs, then let the agent implement it.

## Steps

1. Run `git diff HEAD~1 HEAD --name-only` (or `git diff --staged --name-only` if reviewing staged changes) to see which doc files changed.

2. For each changed doc file, determine what the code needs to do differently:
   - Changes to `docs/system.md` → check if external interfaces or system boundaries need to change
   - Changes to `docs/containers/[name].md` → check if the container's interfaces, technology, or responsibilities need updating in code
   - Changes to `docs/components/[name].md` → check if the component's behavior, interfaces, or structure need implementing or updating
   - Changes to `docs/specs/[name].md` → implement the specified behavior; a spec may affect several components
   - Changes to `docs/ops/[name].md` → bring build, release, deploy, install, or runtime scripts and configuration in line
   - Changes to `docs/external/[name].md` → bring integration code in line with the documented calls, patterns, and limits

3. Read both the updated doc and the current source files before making any code changes.

4. Implement only what the docs describe. Do not add behavior that the docs do not specify.

5. If the docs describe a new component or container with no corresponding code, create it. If the docs remove something, remove the corresponding code only if it is safe to do so.

6. Update code pointers in the doc files if file paths or function names changed during implementation.

## Rules

- The docs define intent; the code must match. If the docs are ambiguous, flag it rather than guessing.
- Do not change docs during this pass (except to update code pointers). If you discover the docs are wrong, report it and ask before changing them.
- Run tests after implementing. If existing tests break, report it — do not silently update tests to match new behavior without flagging the change.

## After implementing

Report what was implemented and what, if anything, was left incomplete or flagged for review.
