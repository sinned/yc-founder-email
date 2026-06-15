# YC Founder Email

A cold(ish) outreach email to **current YC batch founders**, plus the workflow for
personalizing it per-recipient. The live draft is `yc-batch-email.md`.

> **Main repo:** https://github.com/sinned/found-with-claude (lives at
> `../found-with-claude/`). That is the canonical project this email exists to promote;
> this repo (`yc-founder-email`) is a support/outreach satellite. When in doubt about
> the product, the corpus, or the skills, that repo is the source of truth.

## Outreach principles (read before editing copy)

`knowledge/outreach-principles.md` holds the durable copy/outreach principles for this
repo (subject-line strategy, show-don't-tell, lead-with-the-corpus, peer-not-vendor,
the hook rules). This repo is the home for founder/startup outreach going forward, so
treat that file as the standing playbook and keep it current.

## Who's sending it

**Dennis Yang** (sinned@anthropic.com) — 3x founder, now Claude Evangelist at Anthropic.
The "3x founder" credibility is load-bearing: this should read as a peer founder
reaching out, NOT a vendor blast. Protect that tone in every edit.

## What it's promoting

**found-with-claude** — a Claude Code Skills pack for founders, idea → Demo Day.
**This is the main repo:** https://github.com/sinned/found-with-claude (lives at
`../found-with-claude/`).

- 13 skills covering the founder work *the code doesn't cover*: finding the real
  problem, synthesizing customer interviews, stress-testing ideas (simulated customer
  panel), product strategy, prototype scope/review, first-users outreach, PMF signals,
  growth, hiring, fundraising, Demo Day, weekly review. Plus `/new-startup` and `/loop`.
- **The headline value prop = a durable knowledge corpus.** Every skill run deposits
  structured facts (insights, problems, customer segments, decisions) into
  `knowledge/[startup]/` that accumulate run after run. The pitch: your hardest-won
  learning stops dying in Notion/Slack; "by Demo Day you've got receipts, not vibes."
- Sibling repo (the P.S. link): `prototype-with-claude` for founders ready to build
  agents → https://sinned.github.io/prototype-with-claude/getting-started.html

## Decisions already made (don't re-litigate without reason)

- **Audience:** current YC batch. **Goal:** get them to try one skill + give feedback.
  **Tone:** short, casual, founder-to-founder (~200 words).
- **Subject:** `a note from a 3x founder at Anthropic`. Chosen to maximize *opens* by
  a busy YC founder: the from-line (`@anthropic.com`) supplies brand pull, so the
  subject's job is to signal a real human / peer, not a campaign. "3x founder" avoids
  the "founder *of* Anthropic" misread, signals an active track record (not "ex"), and
  reinforces the body's load-bearing credibility. (Prior subject, retired: `"talk to
  users" is only half the advice` — it led with the corpus thesis but read teachy and
  buried the payoff.) NOTE: the subject is now legitimacy-led, not thesis-led, so the
  body's first line + the `[PERSONAL HOOK]` must carry the argument cold. The hook also
  doubles as inbox **preview text**, so front-load its most specific, personal words.
- **No em-dashes.** (User preference — keep them out.)
- **Lead with the corpus**, not a feature list. The user was explicit: the durable
  knowledge corpus is THE key thing.
- **Skill named in the body as the simulation example:** `/synthetic-customer-panel`
  (note: it's a thinking tool, not real research — don't oversell it).
- Email header is styled like a real email (To/From/Subject + horizontal rule).

## The personalization workflow

This is now automated by the **`yc-founder-emails`** skill
(`.claude/skills/yc-founder-emails/`): it reads a LinkedIn connections CSV export
(pre-filtered to YC founders), researches one genuine hook per founder, and writes one
review-ready draft to `emails/` plus an `emails/INDEX.md` send checklist. It never
sends. The CSV and `emails/` are git-ignored (personal contact data). The manual
per-recipient steps below are what the skill does under the hood:

The email opens with a `[PERSONAL HOOK]` slot. Per recipient:
1. Pull the founder's LinkedIn / company / launch (use Claude + web).
2. Draft ONE specific, genuine connection line (mutual contact, their background,
   their launch/post). Must be true and specific. If no real hook exists, CUT the
   line rather than fake it.
3. Fill `[name]` in the To line and greeting.

There's a "How to use this template" block at the top of `yc-batch-email.md` that
must be DELETED before sending.

### Optional idea not yet built
Personalize the *example skill* in paragraph 2 to the founder's stage (discovery-stage
founder → highlight `/customer-discovery-synthesizer`; has-users founder →
`/pmf-signal-review`). Add a `[SKILL CALLOUT]` slot if the user wants this.

## Formatting note

The draft is markdown intended to paste into **Google Docs** (with "Enable Markdown"
on in Docs preferences). Bold/headings/horizontal rules render; the `git clone` block
stays monospace.
