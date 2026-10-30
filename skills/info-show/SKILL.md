---
name: info-show
description: Open the Knowledge-worker project guide or one confirmed local INFO document in the workspace editor.
metadata:
  source: core
  action: Open the main or local INFO document in the workspace editor.
---

# Show Info

## Scope

Use this skill when the user says `Show info` or `Show info {area}`. It opens
the root project guide or requested existing local `INFO.md` in the workspace
editor without changing the workspace.
Primary agent role: information-agent.

## Workflow

1. For `Show info`, open the root `README.md` in the workspace editor.
2. For `Show info {area}`, resolve the named confirmed area and open its
   local `INFO.md` in the workspace editor.
3. State when the requested area has no INFO document or is ambiguous; do not
   create, infer, or modify information while showing it.

## Constraints

- This is read-only.
- Do not create a root `INFO.md` or substitute a local INFO document for the
  project guide.
- Do not treat temporary migration records as durable Knowledge-worker info.
