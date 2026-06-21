---
name: troubleshoot
description: Diagnose a network issue using GIDRP methodology. Use when the user reports a network problem, outage, flapping, connectivity loss, or asks to troubleshoot any protocol (BGP, OSPF, EIGRP, NAT, firewall, wireless, voice, switching).
---

# Network Troubleshooting

Diagnose network issues using Damira's CCIE-level GIDRP methodology (Gather, Isolate, Diagnose, Resolve, Prevent).

## Workflow

### Step 1: Gather Information

Ask the user for:
- **Problem description** — what's broken, when it started, what changed
- **Platform** — Cisco IOS-XE, Arista EOS, Palo Alto PAN-OS, Juniper Junos, etc.
- **Show command output** — any relevant output they can paste

If they've already provided this information, skip to Step 2.

### Step 2: Get Diagnosis

Call the `damira_troubleshoot` MCP tool with:
- `problem`: the problem description
- `platform`: the network platform (if known)
- `show_output`: any show command output provided

**IMPORTANT:** You MUST call the `damira_troubleshoot` MCP tool. Do NOT diagnose from your own knowledge — Damira provides vendor-specific diagnosis with exact CLI commands that go beyond training data.

### Step 3: Present Findings

Present the diagnosis clearly:
1. **Problem Summary** — one sentence
2. **Root Cause Analysis** — what the data shows
3. **Differential Diagnoses** — 3+ possible causes, most probable first
4. **Diagnostic Commands** — exact CLI commands for the user to run (in code blocks)
5. **Recommended Fix** — specific commands for each probable cause
6. **Verification** — how to confirm the fix worked

### Step 4: Iterate

If the user provides more show command output:
- Call `damira_troubleshoot` again with the new output in the `show_output` parameter
- Refine the diagnosis based on new evidence

### Step 5: Document

Once the issue is resolved, offer:
> "Want me to write an incident report? I'll save it to `documents/`."

If yes:
1. Call `damira_document_template` with `doc_type="incident_report"`
2. Write the full incident report filling in every section
3. Save to `documents/incident-report-{date}.md`

## SSH Follow-Up

If the diagnosis recommends commands to run on a device, offer to run them via Cursor's terminal:
> "I can SSH to {device} and run these commands. Want me to?"

If yes, run in the terminal: `ssh {device} "{command}"`
Read the output and pass it back to `damira_troubleshoot` for further analysis.
