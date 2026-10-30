# Knowledge-worker

This workspace is the `Knowledge-worker` base project. It holds the shared
skills and topic-based knowledge structure used by other agent-worker
projects. Temporary migration evidence belongs only in `temp/`.

## Navigation

- Start at [README.md](README.md).
- Read an invoked skill completely before using or changing it.
- Use [skills/INFO.md](skills/INFO.md) for the local skill catalog.
- Use [knowledge/INFO.md](knowledge/INFO.md) for the topic-based knowledge
  base.

## Multi-agent orchestration

Knowledge-worker is a graph-based multi-agent knowledge-maintenance project.
Its orchestrator interprets confirmed public actions, routes work to the
appropriate agent role and bounded skill, reviews the returned evidence, and
either completes the action, requests a decision, or makes an explicit
handoff. It does not authorize external, destructive, or ambiguous changes on
its own.

| Agent role | Responsibility | Skills | Handoffs |
| --- | --- | --- | --- |
| `structure-agent` | Maintain the approved project and agent-control structure. | `project-structure-manage`, `agents-file-manage` | Returns structural evidence to the orchestrator. |
| `skill-agent` | Create, document, and verify bounded reusable capabilities. | `skill-create`, `skill-validate`, `code-document` | Routes catalog changes to `information-agent`. |
| `information-agent` | Maintain and present internal navigation information. | `info-maintain`, `info-show` | Returns requested information or routes knowledge work to `knowledge-agent`. |
| `knowledge-agent` | Create topics and maintain durable, attributed knowledge. | `topic-create`, `info-learn`, `knowledge-base-maintain` | Returns evidence to the orchestrator. |
| `asset-agent` | Classify, retain, and expose approved project-produced assets. | `asset-manage` | Routes public-documentation changes to `publication-agent`; escalates replacement or deletion. |
| `publication-agent` | Maintain external repository documentation and explicit GitHub operations. | `readme-maintain`, `github-maintain` | Escalates external writes and version decisions to the user. |

The deliberation path is always **public action → orchestrator → agent role →
skill workflow → evidence → orchestrator**. The orchestrator may route a
confirmed handoff to another listed role; unclear requirements, conflicts, and
approval-gated work return to the user. These roles are capability nodes in
the project graph, not a claim that persistent external agents are already
running. See the transferable [graph-based multi-agent project model](skills/project-structure-manage/docs/multiagent_project_model.md).

## Info actions

- `Show info` opens the root [README.md](README.md) in the workspace editor.
- `Show info {area}` opens the confirmed area's local `INFO.md` through
  [info-show](skills/info-show/SKILL.md).
- `Maintain assets {request}` invokes
  [asset-manage](skills/asset-manage/SKILL.md) to classify, add, inspect, or
  report on approved project assets.

## Permanent structure

- `skills/` contains complete local skill packages in the approved format.
- `assets/` contains durable project-produced assets. Store infographics in
  `assets/images/`, generated reports in `assets/reports/`, and add other
  clearly named asset subfolders only when their asset type requires one.
- Asset files must have descriptive stable names, retain applicable source or
  generation context with their request or report, and remain in `assets/`.
  Do not replace, relocate, or delete an existing asset without explicit
  approval. Public documentation may reference an approved asset only through
  the `asset-agent` to `publication-agent` handoff.
- Every local skill package uses the lowercase `{target}-{action}` naming
  convention; its folder name and `name` front-matter value must match.
- Every `SKILL.md` uses Codex-compatible top-level front matter: `name`,
  `description`, and optional supported fields only. Knowledge-worker routing
  data belongs in `metadata`; public actions are defined in `AGENTS.md` and
  `README.md`, not as custom Codex front-matter fields.
- Every local skill declares exactly one primary agent role in its `Scope`;
  that role must appear in the Agent graph above.
- `knowledge/` contains durable topic-based knowledge only.
- Knowledge topics and their local records are running-environment content:
  they remain local by default and are not part of a normal GitHub release.
  `knowledge/INFO.md` is the tracked structural stub; its local updates are
  also excluded from a default commit.
- `.env`, `.local/`, `local/`, `runtime/`, and `*.local` are local
  environment material and must never be staged by the GitHub workflow.
- `temp/` contains migration-only material and will be deleted after migration
  acceptance.
- The root `README.md` is the project-level guide. Root `INFO.md` is not used.
  Local INFO documents provide area navigation only.
- Local INFO documents must follow the approved formats in [the info-format
  standard](skills/info-maintain/docs/info_format.md).

## Knowledge topics

Each topic lives at `knowledge/{topic-slug}/` and contains `references/`,
`{topic-slug}_info.md`, `{topic-slug}_ideas.md`, and
`{topic-slug}_refs.md`. Preserve source material in `references/`; record
attributed information in the info record and proposals or questions in the
ideas record.

## Boundaries

- Shared changes require a documented transfer decision; project-specific work
  remains in its owning project.
- Do not retain migration records outside `temp/`.
- Maintain the root `README.md` according to the repository-publication
  declaration below.

## Repository publication

- Repository visibility: `public`.
- README profile: `public-release`.
- README maintenance: reconcile it before every explicitly requested GitHub
  commit using [readme-maintain](skills/readme-maintain/SKILL.md) and the
  [public-release template](skills/readme-maintain/docs/public_release_template.md).

## GitHub actions

- `GitHub {action}` invokes
  [github-maintain](skills/github-maintain/SKILL.md).
- Apply the shared [GitHub version-control standard](skills/github-maintain/docs/version_control.md).

Supported actions are `status`, `connect {owner/repository}`, `commit`,
`commit version`, `commit minor version`, `commit major version`, `commit
knowledge`, and `pull`.

`GitHub commit` and its version variants publish only the approved framework
scope: control documents, managed skills, approved public assets, and external
documentation. `GitHub commit knowledge` is the separate explicit patch-release
action that may include `knowledge/` content and its INFO updates after a
preview. Environment-local paths are never included.

Every commit creates a generated message, a GitHub-controlled semantic release,
and a `{project-slug}_latest.zip` archive that extracts directly into a chosen
destination folder. `commit` defaults to a patch bump; `commit version` and
`commit minor version` use a minor bump; `commit major version` uses a major
bump.

GitHub synchronization is manual only. No action connects, commits, pushes,
pulls, or creates a repository unless the user explicitly requests that action.
