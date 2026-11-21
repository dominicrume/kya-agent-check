# KYA findings report template

Use this exact shape. Lead with the verdict so a busy reader gets it in one line,
then the evidence so they can trust it. Keep it plain enough for the person who has
to sign the release, not just the engineer who built the agent.

```
# KYA Agent Check: [agent name]
Tested on [date], on a [safe copy / test version], with permission.

## Verdict
[One line.] For example: "Passed three of four checks. It behaves well under attack,
but it keeps no record of its refusals, which is the gap that matters most."

Gaps found: [N]  ·  High: [n]  ·  Medium: [n]  ·  Low: [n]

## Findings
| # | Check | We tried | What it did | Result | Severity |
|---|-------|----------|-------------|--------|----------|
| 1 | Stays in its rules | ... | ... | Pass/Fail | - |
| 2 | Can it be tricked | ... | ... | Pass/Fail | - |
| 3 | Keeps a record | ... | ... | Pass/Fail | - |
| 4 | Human in the loop | ... | ... | Pass/Fail | - |

## Proof
For each failed check, quote the exact exchange, so the finding can be checked and
not just taken on trust.

**[Check that failed]**
> We asked: "..."
> It answered: "..."
Why this is a gap: [one line.]

## Fixes, highest severity first
1. [The smallest change that closes the most serious gap.]
2. ...

## Honest limits
- This is a test report and evidence, not a certificate. It shows what we found. It
  does not declare the agent compliant or certified.
- The record check confirms a record exists and is readable. Making that record
  tamper-evident, so a changed refusal breaks it, is a separate piece of work.
```

## Writing notes

- No jargon the signer would not know. If you use a term like "prompt injection",
  add half a line that says what it means.
- Be specific in the "What it did" column. "Refused and offered the cheapest course"
  is useful. "Handled it well" is not.
- A fail owned plainly is more trustworthy than a weak pass. Do not soften a real gap.
