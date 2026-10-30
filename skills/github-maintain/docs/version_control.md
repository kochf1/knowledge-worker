# Shared GitHub Version-Control Standard

This standard is the portable GitHub/version-control package for an
agent-worker project. A project adopts it only when its owner selects GitHub
versioning during structure setup.

## Public Actions

- `GitHub status` inspects state without changing it.
- `GitHub connect {owner/repository}` initializes only the confirmed project
  root and configures a non-conflicting existing or newly approved remote.
- `GitHub commit` creates the default patch release.
- `GitHub commit version` or `GitHub commit minor version` creates a minor
  release.
- `GitHub commit major version` creates a major release.
- `GitHub commit knowledge` creates a patch release that explicitly includes
  the confirmed local knowledge-base content.
- `GitHub pull` fetches and fast-forwards only a clean, non-divergent branch.

## Publication Scope

The default publication scope is the transferable project framework: control
documents, managed skills, approved public assets, and external documentation.
It excludes `knowledge/` and running-environment paths, even when a tracked
knowledge index has changed. `.gitignore` prevents new local knowledge and
environment files from appearing as ordinary candidates, but the commit
workflow must also omit modifications to tracked knowledge files.

`GitHub commit knowledge` is the sole standard action that includes knowledge.
It first reconciles the knowledge structure, previews every knowledge path,
and stages only the user-confirmed set. It may force-add ignored knowledge
files only after that explicit confirmation. Environment-local paths are never
published through either action.

## Version Rules

GitHub semantic tags and releases are the sole version authority. Tags use
`vMAJOR.MINOR.PATCH`. The default initial release is `v0.0.1`; an explicitly
requested initial version is permitted. Each commit action previews the changed
files, generated factual message, and next version before mutation. It then
commits, pushes, creates an annotated tag, pushes the tag, creates a
`{project-slug}_latest.zip` archive from the tag for direct extraction into the
destination folder, and creates a GitHub release with generated notes and that
attached archive.

## Safety Rules

Synchronization is manual. Never force-push, amend, reset, rebase, merge,
discard changes, replace an origin, or change branches. Stop for a dirty tree,
divergence, missing authentication, a different origin, a required merge, or
an ambiguous project root.

## Transfer to Another Project

When GitHub versioning is selected during project setup, copy the complete
`github-maintain` package, including this reference, into the target's local
`skills/` folder. Add its row to `skills/INFO.md`, add the `GitHub {action}`
block to the target `AGENTS.md`, and describe the action in the target root
`README.md`. The target keeps its own remote, GitHub history, tags, releases,
and project-specific pre-commit reconciliation rules. Add the selected default
publication scope and local-runtime ignore rules to the target's `AGENTS.md`
and `.gitignore`.
