# USER.md — User Profiles

> Level 1 core file. Load every session.
> Detailed per-user rules live in the domain tree: `domains/users/`.

## Users

| ID | Name | Domain file |
|----|------|-------------|
| `1285239` | Артём | `domains/users/artem.md` |
| `163037943` | Даша | `domains/users/dasha.md` |

Load the relevant user domain file at session start based on the inbound sender id.
