# YC Founder Email

A cold(ish) outreach email to **current YC batch founders**, plus the workflow for
personalizing it per-recipient. The live draft is `yc-batch-email.md`.

## Who's sending it

**Dennis Yang** (sinned@anthropic.com) — 3x founder, now Claude Evangelist at Anthropic.
The "3x founder" credibility is load-bearing: this should read as a peer founder
reaching out, NOT a vendor blast. Protect that tone in every edit.

## What it's promoting

**found-with-claude** — a Claude Code Skills pack for founders, idea → Demo Day.
Repo: https://github.com/sinned/found-with-claude (lives at `../found-with-claude/`).

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
- **Subject:** `"talk to users" is only half the advice` — riffs on YC canon every
  group partner repeats; sets up the corpus thesis (talking is easy, *retaining +
  acting on it* is the hard half). Body and subject must argue the same point.
- **No em-dashes.** (User preference — keep them out.)
- **Lead with the corpus**, not a feature list. The user was explicit: the durable
  knowledge corpus is THE key thing.
- **Skill named in the body as the simulation example:** `/synthetic-customer-panel`
  (note: it's a thinking tool, not real research — don't oversell it).
- Email header is styled like a real email (To/From/Subject + horizontal rule).

## The personalization workflow (the main remaining work)

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
