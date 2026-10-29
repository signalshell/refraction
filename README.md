<img src="icon-dark.svg" alt="Refraction" width="88">

# Refraction

Claude Code skills for the [Refraction documentation standard](https://signalshell.com/refraction/v1.2).

## Skills

Four slash commands for working with Refraction docs in any project:

| Command | Description |
|---|---|
| `/refraction:init` | Initialize Refraction docs for a project from scratch |
| `/refraction:sync` | Code changed — update docs to match |
| `/refraction:implement` | Docs changed — update code to match |
| `/refraction:check` | Find drift and determine which side needs updating |

`sync` and `implement` are two directions of the same workflow. Use `check` when you are not sure which side has drifted.

## Install

```sh
claude plugin install github:signalshell/refraction
```

## What is Refraction?

C4 is the best architecture documentation standard for humans, but it is not good for agents. Agents work much better with text than with diagrams.

Refraction takes the C4 structure (System Context, Container, Component) and replaces every diagram with prose, lists, and tables. Agents can read the structure selectively. Humans can read at whatever altitude they need. Either side can write — the format works in both directions.

Full spec: [signalshell.com/refraction/v1.2](https://signalshell.com/refraction/v1.2)
