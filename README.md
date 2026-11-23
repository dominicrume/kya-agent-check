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

### Tools exposed by the MCP server (version 1.1.0)
- `kya_get_battery`: Retrieve standard probe batteries for rule compliance, prompt injection, logging, and human escalation.
- `kya_evaluate_exchange`: A keyword SCREEN of one exchange. Returns `flagged`, `not_flagged` or `not_assessed`, never a pass. `not_flagged` is not a pass: a person or model must read the reply and judge it. Record and human checks are always `not_assessed`.
- `kya_generate_report`: Format completed results into a findings report. It refuses unless you give `authorisation` (who owns the agent or permitted the test) and `safe_copy: true`. Both are printed in the report as stated by you, not verified by the tool.
- `kya_seal_report`: Append the report's sha256 to a hash-chained receipt file using the [knowyouragenticai-receipts](https://pypi.org/project/knowyouragenticai-receipts/) package (1.3.1 or later), and print the command that checks it: `python -m knowyouragenticai_receipts verify <file>`. Optional `chain_path` appends to an existing chain; a chain file that does not verify is refused. Without the package it returns `FINGERPRINT_ONLY`, a bare sha256 that is not tamper-evident.

Honest limit of the seal: it shows the report was not edited after sealing only if the chain head is kept somewhere the author does not control. It does not show who made the report or when (the time is the local clock).

The server speaks both the legacy MCP handshake (2024-11-05) and the modern stateless form (2026-07-28, with `server/discover`). Malformed JSON gets a JSON-RPC error, not silence.

Run the tests with `python3 tests/test_server.py` (standard library only; the seal tests need the receipts package importable, set `KYA_PKG_SRC` to its source folder if it is not installed).

---

## One rule

Only run this on an agent you **own** or have **written permission** to test, and
always on a **safe copy** so no real money moves and no real customer is touched.
You are pressing the button on the alarm, not starting a fire.

## What it will not do

It gives you **evidence and fixes**, never a "compliant" or "certified" stamp. It
shows you what it found. Awarding a pass is not its job, and should not be anyone's.

The record check confirms a record exists and is readable. Making the agent's own
record **tamper-evident**, so a changed refusal breaks it, is a separate piece of work.
Sealing the findings report is not the same thing: it protects the report, not the log.

---

Know Your Agentic AI. O'Rume Dominic Uririe. rumedominic.com
