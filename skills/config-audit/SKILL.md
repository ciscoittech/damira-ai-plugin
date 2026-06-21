---
name: config-audit
description: Audit a network device configuration for security issues and best practice violations. Use when the user asks to review, audit, check, or analyze a config file. Also activates when working with files in configs/ directory.
paths: ["configs/**", "**/*.cfg", "**/*.conf"]
---

# Configuration Security Audit

Audit network device configurations for security vulnerabilities and best practice violations.

## Workflow

### Step 1: Get the Config

Two methods:
- **File reference**: User references a file (e.g., `@configs/router.cfg`). Read the file contents.
- **Paste**: User pastes config text directly.

If auditing a directory, read each `.cfg` or `.conf` file and audit them individually.

### Step 2: Run Security Audit

Call the `analyze_config` MCP tool with:
- `config_text`: the full configuration text
- `check_type`: "all" (covers both security and best practices)

**IMPORTANT:** You MUST call the `analyze_config` MCP tool. Do NOT just review the config visually — the tool catches specific patterns (type 7 passwords, SNMP communities, HTTP management, missing NTP) with severity ratings.

### Step 3: Present Findings

Format findings by severity:

**CRITICAL / HIGH:**
- List each finding with line number, issue, and remediation command

**MEDIUM:**
- List each finding with recommendation

**LOW / INFORMATIONAL:**
- List in a table

### Step 4: Remediation

For each finding, provide:
- The **exact CLI command** to fix it (vendor-specific)
- Call `damira_search_vendor_docs` if you need platform-specific remediation syntax

### Step 5: Generate Report (Optional)

If multiple configs were audited, offer:
> "Want me to save the audit report to `documents/`?"

Save as `documents/config-audit-{date}.md` with:
- Summary table (device, findings count by severity)
- Detailed findings per device
- Remediation commands
