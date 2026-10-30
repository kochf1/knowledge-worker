---
name: github-maintain
description: Perform one explicitly requested GitHub connection, status, versioned commit, or pull operation for a confirmed project.
metadata:
  source: core
  action: Connect, inspect, versioned commit, or pull one project on explicit request.
---

# Maintain GitHub

## Scope

Use this skill when the user says `GitHub {action}` for one confirmed project.
Supported actions are `status`, `connect {owner/repository}`, `commit`,
`commit version`, `commit minor version`, `commit major version`, `commit
knowledge`, and `pull`.
Every commit action generates a concise message from the changed files and
creates a GitHub-controlled semantic version release. It never synchronizes
automatically. Apply the portable
[version-control standard](docs/version_control.md).
Primary agent role: publication-agent.

## Workflow

1. Read `docs/plan.md`, the target project's `AGENTS.md`, and its root
   `README.md`. Confirm the exact project root and requested GitHub action.
2. For `status`, inspect and report the local Git root, origin, branch,
   upstream, working-tree state, and available ahead/behind information without
   changing state.
3. For `connect {owner/repository}`, inspect local Git and GitHub access. On
   the explicit request, initialize Git only at the confirmed project root,
   create the named GitHub repository only when it is absent and the user has
   explicitly selected public or private visibility, then configure a
   non-conflicting `origin`. Do not commit, push, or pull.
4. For a normal commit action, invoke `readme-maintain` only when the declared
   profile requires it. Stage and publish only the approved framework scope:
   control documents, managed skills, approved public assets, and external
   documentation. Exclude all `knowledge/` changes and ignored local-runtime
   paths, including a tracked `knowledge/INFO.md` change.
5. For `commit knowledge`, first invoke `knowledge-base-maintain`, then
   preview the exact knowledge files to include. Stage the confirmed knowledge
   scope explicitly, including ignored topic files only when the user has
   confirmed their inclusion. Never include local-runtime paths.
6. For either commit action, confirm the branch and upstream, inspect the
   selected files, and generate a concise factual commit message. Preview the
   proposed changed files, message, and next version before mutation. Commit
   and push the confirmed project changes, create and push an annotated
   semantic tag, create `{project-slug}_latest.zip` from that tag for direct
   extraction into the destination folder, attach it when creating the GitHub
   Release with generated notes, and remove the temporary archive after a
   successful upload.
7. Determine the requested version bump under the version-control standard.
   Use the latest GitHub semantic release/tag as the version authority; an
   explicitly requested initial version may override the default `v0.0.1`.
   Do not create a local VERSION file or changelog.
8. For `pull`, fetch remote information and report divergence. On the explicit
   request, fast-forward only when the working tree is clean and no merge or
   rebase is required.
9. Report factual resulting state, including any commit, version, release URL,
   or revision identifier,
   or escalate when the requested operation is unsafe or ambiguous.

## Constraints

- Never perform an action not explicitly named by the user.
- Never create a GitHub repository without an explicit public/private choice.
- Never replace an existing origin, amend, force-push, merge, rebase, reset,
  discard changes, or change branches.
- GitHub tags and releases are the authoritative version records; never create
  a local VERSION file or changelog.
- A normal commit stages only selected framework files after previewing them;
  it excludes `knowledge/` even when a tracked knowledge file is modified.
  `commit knowledge` stages knowledge only after an explicit preview and
  confirmation of its contents. Escalate an ambiguous or unsafe scope.
- Never synchronize automatically after local changes, connection, or on a
  schedule.
- Escalate missing authentication, insufficient permission, an ambiguous root,
  a different existing origin, unapproved files, a dirty tree, divergence, or
  any required merge or rebase.
