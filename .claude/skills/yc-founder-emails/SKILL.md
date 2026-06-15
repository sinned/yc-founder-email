---
name: yc-founder-emails
description: Hydrate a flight of personalized YC founder outreach emails from a LinkedIn connections CSV, using the yc-batch-email.md template. Researches one genuine hook per founder and writes one review-ready draft file each. Trigger phrases: "hydrate the founder emails", "draft the YC flight", "personalize the batch email", "make the founder outreach drafts".
---

# YC Founder Emails

Turns a list of YC founder connections (a LinkedIn connections CSV export) into a
flight of individually personalized outreach emails, each introducing the founder to
**found-with-claude** (https://github.com/sinned/found-with-claude).

This skill does NOT send anything. It writes one review-ready markdown draft per
founder to `emails/`, plus an index, so Dennis can read every draft and send them
himself.

## What this protects

The email is from Dennis Yang, 3x founder, now Claude Evangelist at Anthropic. The
"3x founder" framing is load-bearing: every draft must read as a peer founder
reaching out, NOT a vendor blast. The rules in the repo `CLAUDE.md` are binding:
- **No em-dashes.** Ever.
- Lead with the durable knowledge corpus, not a feature list.
- Subject and body argue the same point ("talking is easy, retaining + acting on it
  is the hard half").
- The hook must be **true and specific**. If no real hook exists, CUT the line. Never
  fabricate a connection, a mutual, a launch, or a detail.

## Input

1. **The template** — `yc-batch-email.md` in the repo root. This is the single source
   of truth for body copy, subject, sign-off, and the P.S. Read it fresh every run;
   do not hardcode the copy into this skill.
2. **The connections CSV** — a LinkedIn data export (Settings > Data Privacy > Get a
   copy of your data > Connections). Ask the user for the path if not given. Expected
   columns (LinkedIn's export format):

   ```
   First Name,Last Name,URL,Email Address,Company,Position,Connected On
   ```

   Real exports sometimes prepend 2-3 "Notes:" lines before the header. Skip to the
   row that starts with `First Name`. Email Address is often blank (LinkedIn hides it
   unless the connection allowed export); that is expected.
3. **The recipient list is pre-filtered.** Treat every row in the CSV as a founder to
   email. This skill does NOT decide who is a YC founder; the user hands it the
   already-filtered list. If a row is obviously not a founder (e.g. title is
   "Recruiter"), flag it in the run summary but still draft unless told otherwise.

## Steps

1. **Read the template** (`yc-batch-email.md`) and the repo `CLAUDE.md` so the tone
   rules and current copy are in context.

2. **Parse the CSV.** Skip any leading notes lines, find the `First Name` header, and
   build one record per row: `{ name, company, title, linkedin_url, email }`. Report
   the count back to the user before drafting ("Found 23 connections. Drafting 23
   emails."). De-duplicate by LinkedIn URL.

3. **Per founder, research ONE hook.** Use `WebSearch` / `WebFetch` (and the LinkedIn
   URL, company name, and any public launch) to find one specific, genuine connection
   point. Prefer, in order:
   - A mutual person or shared company/org in their background.
   - Their YC launch, product, or a recent post/announcement.
   - A specific, non-generic detail of their background that this corpus is built for
     ("you spent 6 years in clinical ops before starting X").

   The hook is ONE sentence, true and specific. **If you cannot verify a real hook,
   set the hook to empty and drop the `[PERSONAL HOOK]` line entirely for that draft.**
   A clean no-hook email beats a fake or generic one ("Congrats on the launch!" with
   no specifics is a fake hook; cut it). Record the source URL you used in the
   draft's frontmatter so it can be spot-checked.

4. **(Optional) Tailor the example skill to their stage.** Only if the user asked for
   it (see "Stage-based skill callout" below). Discovery-stage founder ->
   `/customer-discovery-synthesizer`; has-users founder -> `/pmf-signal-review`.
   Otherwise leave the body's example skill as written in the template.

5. **Hydrate the template.** Fill `[name]` in the To line and greeting, drop in the
   hook line (or remove it), and **delete the "How to use this template" instruction
   block** at the top. The output is a real email, not a template.

6. **Write one file per founder** to `emails/<firstname>-<lastname>.md` (lowercase,
   kebab). Each file starts with a small frontmatter block for review, then the
   hydrated email:

   ```markdown
   ---
   to: Jane Doe <jane@acme.com>   # or "Jane Doe (no email in export)"
   company: Acme
   linkedin: https://linkedin.com/in/jane
   hook_source: https://...        # URL the hook was verified from, or "none"
   hook: present | cut (no genuine hook found)
   ---

   [hydrated email body]
   ```

7. **Write `emails/INDEX.md`** — a review checklist: one row per founder with name,
   company, whether a hook was found, the hook source link, and whether an email
   address was present. This is Dennis's send queue.

8. **Report a run summary** — total drafted, how many got a real hook vs cut, how many
   are missing an email address, and any rows flagged as probably-not-founders.

## Stage-based skill callout (optional)

Off by default. If the user says "tailor the skill to each founder's stage", swap the
example skill named in paragraph 2 of the body:
- **Discovery stage** (pre-launch, still finding the problem) -> `/customer-discovery-synthesizer`
- **Has users / launched** -> `/pmf-signal-review`
- **Unknown** -> leave the template default.

Infer stage from the hook research (their launch status, what their site says). When
unsure, do not guess; use the default.

## Hook quality bar

**Cut it (fake / generic):**
- "Congrats on the launch!" (no specific detail)
- "Love what you're building." (true of anyone)
- "Saw we're both in YC." (not personal)

**Keep it (true + specific):**
- "We both overlapped with Priya at Stripe."
- "Your Demo Day launch of the clinical-notes tool is exactly the messy-transcript
  problem this is built for."
- "You spent 6 years in logistics before starting Freightline; that hard-won context
  is the kind that usually dies in Slack."

The test: could this sentence be copy-pasted into another founder's email unchanged?
If yes, it is generic. Cut it.

## Guardrails

- **Never fabricate.** No invented mutuals, launches, quotes, or background. Unverified
  = cut the hook.
- **No em-dashes** in any draft. Re-scan output for `—` before finishing.
- **Do not send.** This skill only writes files. Sending is Dennis's manual step.
- **Volume sanity:** if the CSV has more than ~50 rows, confirm the count with the
  user before drafting the full flight (research is web-call heavy).
- **Preserve the template's argument.** Do not rewrite the body's thesis per founder;
  only the hook line (and optionally the one example-skill name) changes between
  drafts. Everything else stays as the template defines it.
- **Privacy:** the CSV holds personal contact data. Keep it local; do not post names,
  emails, or the list to any external service beyond the targeted public web lookup
  needed for the hook.

## Output

```
emails/
  INDEX.md              # review + send checklist, one row per founder
  jane-doe.md           # hydrated, ready to read and send
  sam-lee.md
  ...
```
