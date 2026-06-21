---
name: upgrade-plan
description: Plan a network product upgrade with risk assessment and MOP generation. Use when the user asks to upgrade, migrate, or update any network platform version (CUCM, IOS-XE, NX-OS, PAN-OS, FortiOS, Junos, ISE, ASA).
---

# Upgrade Planning

Plan network product upgrades with structured risk assessment and generate production-ready MOPs.

## Workflow

### Step 1: Gather Requirements

Ask the user for:
- **Product** — e.g., CUCM, IOS-XE, PAN-OS, FortiOS, Junos
- **Current version** — e.g., 17.6.3, 12.5 SU7, 10.2.4
- **Target version** — e.g., 17.9.4, 15.0, 11.1.3
- **Environment** — device count, role (core/edge), production/lab, user count

If they've already provided this, skip to Step 2.

### Step 2: Research (3 MCP Tool Calls)

Call these MCP tools in sequence:

**1. Upgrade assessment:**
Call `damira_upgrade_plan` with product, current_version, target_version, environment.

**2. Security check:**
Call `damira_search_cve` with the target version to check for known vulnerabilities.

**3. Release notes:**
Call `damira_search_release_notes` with product and target version for known bugs and caveats.

**IMPORTANT:** You MUST call all three MCP tools. Do NOT skip the CVE or release notes check — customers need the full picture before upgrading.

### Step 3: Present Assessment

Combine findings from all three tools into a structured assessment:
1. **Upgrade Path** — direct or stepping stones required
2. **Prerequisites** — hardware, disk space, backups, licenses
3. **Security Advisories** — CVEs fixed or introduced in target version
4. **Known Bugs** — caveats from release notes
5. **Risk Level** — low/medium/high with justification
6. **Estimated Maintenance Window** — realistic duration
7. **Rollback Procedure** — specific steps and trigger criteria

### Step 4: Generate MOP

Offer:
> "Want me to write the full MOP? I'll save it to `documents/`."

If yes:
1. Call `damira_document_template` with `doc_type="mop"` to get the required sections
2. Write the complete MOP filling in every section with data from the upgrade assessment
3. Every step must have expected output
4. Rollback must have specific trigger criteria
5. Save to `documents/{product}-upgrade-mop-{current}-to-{target}.md`

### Step 5: Generate Change Control (Optional)

If the user asks:
1. Call `damira_document_template` with `doc_type="change_control"`
2. Write the change control with RFC fields, risk matrix, CAB checklist
3. Save to `documents/{product}-change-control.md`
