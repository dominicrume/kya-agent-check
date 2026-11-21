# KYA Agent Check

Press the button on your AI agent, on purpose, before a customer or an attacker
does. A drop-in check that runs inside the agent you already use.

It tests what your agent **does when it runs**: does it refuse the dangerous action,
can it be tricked, does it keep a record you can read later, does a human step in.
Then it writes a findings report with the proof and the fix for each gap.

This checks **behaviour**, not code. For the code your AI wrote, use a code scanner
like the AI Code Quality Auditor instead. The two are different jobs. Keep them apart.

---

## Quickstart: Use as a Skill

### Claude Code
Clone or copy this folder into your skills directory:
```bash
git clone https://github.com/dominicrume/kya-agent-check.git ~/.claude/skills/kya-agent-check
```

### Cursor
Drop `.cursorrules` into your project root, or copy the `kya-agent-check` folder into your workspace rules.

### Run your first check
In your agent, just say:
```
Run the KYA check on my chatbot.
```

It will ask for two things, then do the rest:
- How it reaches your agent (a chat window, a test endpoint, or pasted transcripts).
- Your agent's must-never list (the few things it is not allowed to do).

---

## Phase 2: Use via MCP (Model Context Protocol)

Connect the KYA Agent Check directly to any tool that speaks MCP:

### Claude Code
```bash
claude mcp add kya-agent-check -- python3 /path/to/kya-agent-check/kya_agent_check_mcp.py
```

### Claude Desktop
Add to your `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "kya-agent-check": {
      "command": "python3",
      "args": ["/absolute/path/to/kya-agent-check/kya_agent_check_mcp.py"]
    }
  }
}
```

### Tools exposed by the MCP server
- `kya_get_battery`: Retrieve standard probe batteries for rule compliance, prompt injection, logging, and human escalation.
- `kya_evaluate_exchange`: Evaluate an exchange against must-never rules and output severity, proof, and the smallest fix.
- `kya_generate_report`: Format completed results into an executive-ready findings report.
- `kya_seal_report`: Cryptographically seal the report into a tamper-evident SHA-256 receipt.

---

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
