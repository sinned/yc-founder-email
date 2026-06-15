# yc-founder-email

Outreach to **current YC batch founders** introducing them to
[**found-with-claude**](https://github.com/sinned/found-with-claude), a Claude Code
skills pack for the founder work the code doesn't cover (idea to Demo Day).

> **Main repo:** https://github.com/sinned/found-with-claude. That is the canonical
> project this email exists to promote. This repo is a support / outreach satellite.

## What's here

- **`yc-batch-email.md`** — the live email draft. A short, founder-to-founder note
  (~120 words) leading with the durable knowledge corpus that found-with-claude builds.
  It contains a `[PERSONAL HOOK]` slot and `[name]` placeholders to fill per recipient,
  plus a "How to use this template" block that is deleted before sending.
- **`crm/`** — a file-based CRM for the outreach. One markdown file per contact
  (`crm/contacts/<slug>.md`) is the source of truth: facts, hook, the email draft, and a
  dated log; `crm/pipeline.md` is the board. Real records and the board are git-ignored
  (this repo is public); only the system + a fake `_example.md` are committed. See
  `crm/README.md`.
- **`.claude/skills/yc-founder-emails/`** — a Claude Code skill that hydrates a *flight*
  of these emails from a LinkedIn connections CSV export: it reads the template,
  researches one genuine hook per founder, writes a CRM contact record (with the
  ready-to-send draft) per founder into `crm/contacts/`, and refreshes the board. It
  never sends.
- **`sample-connections.csv`** — a tiny fixture in LinkedIn export format for dry-running
  the skill.
- **`CLAUDE.md`** — project instructions and the decisions already made (tone, subject,
  no em-dashes, lead-with-the-corpus). Read this before editing the email.

## Sending a flight

1. Export your connections from LinkedIn (Settings > Data Privacy > Get a copy of your
   data > Connections), and trim the CSV to the YC founders you want to reach.
2. In Claude Code, run the skill: *"hydrate the founder emails from `<path-to-csv>`"*.
   It creates a CRM record per founder in `crm/contacts/` and refreshes `crm/pipeline.md`.
3. Review each draft in its contact record, verify every hook is true and specific, send
   it yourself, then update the contact's `status` and log.

## Privacy

This repo is **public.** `Connections.csv`, the generated `emails/`, all real CRM
contact records (`crm/contacts/*` except `_example.md`), and `crm/pipeline.md` hold
personal contact data and are git-ignored. Keep them local; do not commit them. If you
want the CRM data version-controlled, make the repo private first.
