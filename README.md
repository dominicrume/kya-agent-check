# KYA Agent Check

Press the button on your AI agent, on purpose, before a customer or an attacker
does. A drop-in check that runs inside the agent you already use.

It tests what your agent **does when it runs**: does it refuse the dangerous action,
can it be tricked, does it keep a record you can read later, does a human step in.
Then it writes a findings report with the proof and the fix for each gap.

This checks **behaviour**, not code. For the code your AI wrote, use a code scanner
like the AI Code Quality Auditor instead. The two are different jobs. Keep them apart.

## 60-second quickstart

**1. Install it into your agent.**

Claude Code (drop-in skill):
```
# clone or copy this folder into your skills directory
cp -r kya-agent-check ~/.claude/skills/
```

Cursor or any agent that reads a skills folder: put the `kya-agent-check` folder
where that tool loads skills, or paste `SKILL.md` into your project.

**2. Run your first check.** In your agent, just say:
```
Run the KYA check on my chatbot.
```

It will ask for two things, then do the rest:
- how it reaches your agent (a chat window, a test endpoint, or pasted transcripts),
- your agent's must-never list (the few things it is not allowed to do).

**3. Read the report.** You get a one-line verdict, a pass or fail per check, the
exact exchange as proof, and the fix for each gap.

## One rule

Only run this on an agent you **own** or have **written permission** to test, and
always on a **safe copy** so no real money moves and no real customer is touched.
You are pressing the button on the alarm, not starting a fire.

## What it will not do

It gives you **evidence and fixes**, never a "compliant" or "certified" stamp. It
shows you what it found. Awarding a pass is not its job, and should not be anyone's.

The record check confirms a record exists and is readable. Making that record
**tamper-evident**, so a changed refusal breaks it, is a separate piece of work.

---

Know Your Agentic AI. O'Rume Dominic Uririe. rumedominic.com
