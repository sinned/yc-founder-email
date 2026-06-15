# File-based CRM

A plain-markdown CRM for founder/startup outreach. One file per contact is the single
source of truth: it holds the contact's facts, the personalization hook, the full email
draft, and a dated interaction log. `pipeline.md` is the roll-up board across everyone.

This is the same idea as the found-with-claude knowledge corpus: structured facts in
files that accumulate over time, no SaaS, greppable, diff-able, yours.

## Privacy (important: this repo is public)

Real contact records and the live board contain personal data (names, emails, who you
contacted, who passed). **They are git-ignored and must stay local.** Only the *system*
is committed: this README, `_template.md`, and `contacts/_example.md` (a fake contact).

Git-ignored, never commit:
- `crm/contacts/*.md` (except `_example.md`)
- `crm/pipeline.md`

If you ever want the data version-controlled, make the repo private first.

## Layout

```
crm/
  README.md            # this file (committed)
  _template.md         # blank contact record (committed)
  contacts/
    _example.md        # fully worked fake example (committed)
    jane-doe.md        # one file per real contact (LOCAL, git-ignored)
    ...
  pipeline.md          # the board: everyone by status + next action (LOCAL, git-ignored)
```

## Contact record

Each `contacts/<first>-<last>.md` starts with frontmatter, then sections. See
`_template.md` for the blank and `contacts/_example.md` for a filled-in one.

Frontmatter fields:

| field | meaning |
|---|---|
| `name` | Full name |
| `company` | Company |
| `title` | Their role |
| `linkedin` | Profile URL |
| `email` | Email, or empty if not in the LinkedIn export |
| `batch` | YC batch if known (e.g. `YC W26`), else blank |
| `stage` | `discovery` \| `has-users` \| `unknown` (drives which skill to highlight) |
| `status` | funnel stage, see below |
| `hook_source` | URL the hook was verified from, or `none` |
| `next_action` | the next concrete thing to do (e.g. `send`, `follow-up`) |
| `next_action_date` | when to do it (YYYY-MM-DD) |
| `last_touch` | date of the most recent interaction |
| `tags` | freeform list, e.g. `[yc, healthtech]` |

## Status funnel

Move a contact forward by editing `status` and appending a dated line to its log.

| status | meaning |
|---|---|
| `new` | imported, no hook/draft yet |
| `researched` | hook found (or deliberately cut); ready to draft |
| `drafted` | email written, awaiting your review |
| `sent` | email sent |
| `replied` | they wrote back |
| `meeting` | call/meeting booked |
| `tried` | they actually ran the repo / gave feedback (the goal) |
| `passed` | declined or not interested |
| `no-response` | sent, went cold |
| `bounced` | bad email address |

## Daily use

- **What do I do today?** Grep for actions that are due:
  `grep -rl "next_action_date: 2026-06-" crm/contacts/` or scan `pipeline.md`.
- **Log every touch.** Append `- YYYY-MM-DD — what happened` to the contact's `## Log`,
  and update `last_touch` + `status` + `next_action(_date)`.
- **Regenerate the board.** Ask Claude to refresh `pipeline.md` from the contact files,
  or maintain it by hand.

## How the email skill plugs in

The `yc-founder-emails` skill imports a LinkedIn connections CSV and creates one
`contacts/<slug>.md` per founder: it researches the hook, writes the hydrated draft into
the record's `## Draft` section, sets `status: drafted`, and refreshes `pipeline.md`. It
never sends. You review each draft in its record, send it yourself, then update status.

## pipeline.md format

The board is a status-grouped table. Example (with the fake `_example` contact):

```markdown
# Pipeline
*Updated: 2026-06-15 | 1 contact*

## Drafted (1)
| name | company | next action | due | hook? |
|---|---|---|---|---|
| Jane Doe | Acme | send | 2026-06-18 | yes |

## Sent (0)
## Replied (0)
## Tried (0)
```
