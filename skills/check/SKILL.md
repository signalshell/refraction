---
description: Check whether Refraction documentation is consistent with the current code. Uses git history to determine which side is authoritative for each discrepancy. Reports whether to run sync or implement.
---

Check whether this project's Refraction documentation is consistent with the current code, and whether the docs follow the Refraction documentation standard v1.2 (https://signalshell.com/refraction/v1.2).

## Steps

1. Check if `docs/system.md` exists.
   If not, report that Refraction is not initialized and suggest running `/refraction:init`.

2. Verify structure and markers:
   - every file under `docs/` has the correct marker at the top: `<!-- L1: System Context -->`, `<!-- L2: Container -->`, `<!-- L3: Component -->`, `<!-- L4: Spec -->`, `<!-- Ops -->`, `<!-- External -->`; report missing or wrong markers
   - `docs/system.md` links to every container, and every container links to its components
   - every file is reachable from `docs/system.md` by following links; report orphan files

3. Verify code pointers: file paths and function names in component and spec files still exist in the codebase.
   Check the referenced file directly or run a targeted search.

4. Verify constants: for each constant documented together with a value, compare that value against the code where the name is defined.

5. Scan the doc files for standard violations:
   - the same fact written in two doc files; report both files and say which file should own it (the lowest layer that owns the fact)
   - history narrative such as "used to" or past-tense accounts of earlier behavior
   - lines that wrap at a fixed column instead of following one sentence per line
   - hand-maintained diagrams (Mermaid, PlantUML, ASCII art)
   - images that are undated, do not say what they show, or carry a fact that is not also written in the text

6. Check agent instruction files such as `AGENTS.md` and `CLAUDE.md`: they must link to `docs/system.md` for architecture instead of restating it.
   Report any restated architecture.

7. Scan for obvious drift:
   - new source files or directories that do not correspond to any documented component
   - interfaces mentioned in docs that no longer exist in the code (changed endpoint paths, removed CLI flags, renamed config fields)

8. For each code-vs-doc discrepancy, check git history to determine which side changed more recently:
   - run `git log -1 --format="%ci %s" -- <doc-file>` for the doc file
   - run `git log -1 --format="%ci %s" -- <source-file>` for the relevant source file
   - if the source file changed more recently: the docs are stale; suggest running `/refraction:sync`
   - if the doc file changed more recently: the code has not caught up; suggest running `/refraction:implement`
   - if both changed at the same time or the signal is ambiguous: flag it explicitly

9. Report code-vs-doc discrepancies in three categories:
   - **Docs are stale** — code changed after the docs; run `/refraction:sync`
   - **Code has not caught up** — docs changed after the code; run `/refraction:implement`
   - **Uncertain** — both sides changed around the same time, or the discrepancy cannot be attributed to either

10. Report standard violations (duplicated facts, orphans, missing or wrong markers, fixed-column wrapping, history narrative, restated architecture, diagram use, image rules) separately from the three categories; they are always doc fixes, so suggest running `/refraction:sync` for them.

## Rules

- Do not modify any files during this check — report only.
- Flag uncertainty explicitly.
  "I could not determine which side is authoritative" is more useful than a wrong verdict.
