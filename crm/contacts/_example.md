---
name: Jane Doe
company: Acme
title: Co-founder & CEO
linkedin: https://www.linkedin.com/in/janedoe
email: jane@acme.com
batch: YC W26
stage: discovery
status: drafted
hook_source: https://www.acme.example/launch
next_action: send
next_action_date: 2026-06-18
last_touch: 2026-06-15
tags: [yc, healthtech]
---

# Jane Doe — Acme

> NOTE: This is a FAKE example contact, committed to show the record format. Real
> contact records live alongside it but are git-ignored. Do not treat this as a real
> person.

**Hook:** Your Demo Day launch of the clinical-notes tool is exactly the messy-transcript
problem this is built for.

## Log
- 2026-06-15 — imported from LinkedIn connections export.
- 2026-06-15 — researched hook, verified via the Acme launch page. Stage read as
  discovery (pre-revenue, still scoping the problem).
- 2026-06-15 — draft written. status: drafted. Next: send 06-18.

## Draft

**To:** Jane Doe <jane@acme.com>
**From:** Dennis Yang <sinned@anthropic.com>
**Subject:** a note from a 3x founder at Anthropic

Hey Jane,

Your Demo Day launch of the clinical-notes tool is exactly the messy-transcript problem this is built for.

You'll do a hundred user calls this batch. Then a partner asks what you've actually learned, and you're scrolling three weeks of call notes trying to remember who said the thing that mattered. I've done this three times: the hard part was never the code. It's holding onto what they told you and acting on it before it's gone.

I built **found-with-claude** for that: 13 Claude Code skills for the work the code doesn't cover (finding the real problem, synthesizing interviews, prepping Demo Day). The part I care about: every run deposits what you learned into a **durable knowledge corpus**, structured facts that pile up run after run. Your hardest-won learning stops dying in Notion tabs and Slack threads. By Demo Day you've got receipts, not vibes.

Takes 30 seconds to try:

```
git clone https://github.com/sinned/found-with-claude
claude
/new-startup
```

Point one skill at something real and tell me what was useful and what broke. I'd take brutal over polite any day.

Dennis
3x founder, now Claude Evangelist at Anthropic

**P.S.** Already building agents? → https://sinned.github.io/prototype-with-claude/getting-started.html

## Notes

- Discovery stage, so if tailoring the example skill by stage, highlight
  `/customer-discovery-synthesizer`.
- Mutual: none verified. Hook is launch-based, which is fine.
