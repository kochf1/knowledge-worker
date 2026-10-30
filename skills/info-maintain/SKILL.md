---
name: info-maintain
description: Rebuild local project and skills info documents when maintained records or QA evidence change.
metadata:
  source: core
  action: Rebuild maintained info documents.
---

# Maintain Info

## Scope

This is an internal skill. Use it after Knowledge-worker project records,
managed skills, or QA evidence change. It is responsible only for maintaining
approved local INFO formats from authoritative records. Its inputs are current
`AGENTS.md`, maintained skill definitions, topic folders, and QA records; it
produces refreshed skills, knowledge, or topic-local `INFO.md` files. It has no
user activation command; a calling workflow invokes it.
Primary agent role: information-agent.

## Workflow

1. Read the relevant maintained records and confirm each entry has a verified
   source; ask for clarification when ownership or scope is ambiguous.
2. Select the local info document to maintain: skills, knowledge, or a
   topic-local document. Apply the exact applicable format in
   [info_format.md](docs/info_format.md).
3. For `skills/INFO.md`, retain only the required title and the five-column
   skill table. Do not retain narrative or legacy columns. Do not create or
   maintain a root `INFO.md`; project-level guidance belongs in `README.md`.
4. Check that every linked target exists; derive each skills-table Action from
   the package's `metadata.action` value and derive status, plan, and QA links
   from its managed package. Report missing evidence as `PENDING`, rather than
   inferring a result.
5. Produce the refreshed info document. Deprecated implementation material is
   retained only under `temp/migration/` and must not be used to overwrite the
   approved formats.

## Constraints

- Do not edit a requirement, plan, skill definition, or QA record to make an info document look complete.
- Do not manufacture a passing status; the info document reports recorded evidence only.
- Do not add sections, prose after the skills table, role classifications, or
  retired metadata to local INFO documents.
- Non-goals include creating skills, changing project behavior, and deciding missing source facts.
