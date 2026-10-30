# Knowledge-worker INFO Format

This is the authoritative format for Knowledge-worker local INFO documents.
`info-maintain`, `skill-create`, and `skill-validate` apply it whenever they
create, revise, or check a local INFO document. Root `INFO.md` is not used;
the root `README.md` is the project-level guide.

## Skills INFO

The local file is named `skills/INFO.md`. It contains exactly the title below
and one table, with no description before the table and no content after it:

```md
# SKILLS Info

| Skill | Action | Status | Plan | QA |
| --- | --- | --- | --- | --- |
| [skill-name](skill-name/SKILL.md) | Bounded action. | PENDING | [Plan](skill-name/docs/plan.md) | [QA](skill-name/docs/qa.md) |
```

List every managed local skill once, alphabetically by its folder name. The
Status value is evidence-based (`VERIFIED`, `PENDING`, `FAILED`, or another
documented current state); it is never inferred from a missing or stale QA
record. The Action value comes from the corresponding package's
`metadata.action` value; it does not define or activate a public user action.
