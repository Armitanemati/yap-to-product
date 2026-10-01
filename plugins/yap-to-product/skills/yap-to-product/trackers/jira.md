# Tracker adapter: Jira

Read this before any Jira call. It maps the board model and rules in `SKILL.md` to Jira.

## Requirements

- A Jira Cloud site (guide B in `references/guided-setup.md` if the user has none)
- A Jira connection available to Claude (guide D)

## What the connection can and cannot do

Typical Jira connections can: list visible projects, read issue type metadata, search with JQL, create and edit issues, comment, link issues, read available transitions, and transition issues.

Many cannot create projects, add statuses, or edit workflows. If yours cannot, the user does this once with guide C. Optional: add a "Won't Do" resolution or status for declined tasks.

## Session start checks

1. Confirm the site and project key with the user. Do not guess between several projects.
2. Read the issue types for the project (Epic and Task or Story must exist).
3. Read the available transitions on one existing issue. If the project is empty, create the first epic only after the preview is approved, then read its transitions.
4. If a required status is missing, stop, name it, and offer guide C or the closest mapping (for example "Backlog" for "For Future"). Use a mapping only if the user agrees.

## Mapping

| Board model | Jira |
|---|---|
| Epic | Issue type Epic |
| Task | Issue type Task or Story, linked to its epic |
| Columns | Statuses with the same names, or the mapping the user approved |
| Labels | Lowercase, hyphenated: `mvp`, `future`, `scalability`, `legal`, `security`, `infra`, `launch`, `needs-thinking`, `assumption`, `needs-professional-review`, `wont-do` |
| Scalability epic priority | "Lowest" (or the lowest available) |
| Dependency | Issue link "is blocked by" |

**Linking tasks to epics.** Team-managed projects use the Parent field; some company-managed projects use an Epic Link field. Read the create metadata to see which exists; if unclear, ask once.

**New items land in the default status.** After creating an item, transition it to the intended column using the transition list. Never assume transition IDs; read them.

## Working by key and reporting stages

Jira keys look like `AR-1`: the project key, a hyphen, and a number. When the user says "start AR-1", read that issue, transition it to In Progress, and report by key from then on.

Jira statuses only show the workflow column. Track the deployment stage with labels as well, so a report is accurate:

| Stage (SKILL.md section 9) | Jira status | Label |
|---|---|---|
| Not started | To Do or For Future | none |
| In progress | In Progress | none |
| Built, not deployed | In Progress | `built` |
| On staging, needs QA | Testing (or In Progress if no Testing column) | `on-staging`, `needs-qa` |
| In production | Testing or Done | `in-production` |
| Blocked | unchanged | `blocked`, plus a comment with the reason and an "is blocked by" link when another issue is the cause |
| Done | Done | none |

Replace stage labels as work moves (remove `built` when adding `on-staging`). Remove `blocked` when the blocker clears. Add a short comment at each stage change: what changed and how to check it.

To answer "where is AR-1?", read the issue's status, labels, and latest comment, then reply with key, title, and stage in one line, plus the next action.

To report on everything in progress:

```
project = ABC AND statusCategory != Done ORDER BY updated DESC
```

## Searching for an existing epic

```
project = ABC AND issuetype = Epic AND (summary ~ "share*" OR summary ~ "invite*" OR labels in (sharing)) ORDER BY updated DESC
```

Replace `ABC` with the confirmed key and adjust the terms. If several epics match, list them and ask.

## Declined tasks

1. Comment "Declined by user".
2. Add the label `wont-do`.
3. Transition to Done, with resolution "Won't Do" if the project offers it.

## Enforcing "humans move to Done"

Claude follows the status rules, but Jira does not enforce them, because the connection acts with the user's own permissions. A Jira admin can add a condition to the transitions into Testing and Done (for example restricting them to a group). Mention this once; do not change workflow settings yourself.

## Formatting

Short paragraphs, bullet lists, and code blocks for prompts. If a format is rejected, fall back to plain text and keep prompts in a clearly marked block.
