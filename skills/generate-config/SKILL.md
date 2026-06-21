---
name: generate-config
description: Generate network device configuration files. Use when the user asks to create, write, or generate a config for any network device (router, switch, firewall, wireless controller).
---

# Network Config Generation

Generate production-ready device configuration files.

## Workflow

### Step 1: Gather Requirements

Ask the user for:
- **Device type** — e.g., Cisco ISR4451, Arista 7050X, Palo Alto PA-3260, Juniper MX204
- **Platform/OS version** — e.g., IOS-XE 17.9, EOS 4.28, PAN-OS 11.1
- **Features** — e.g., BGP peering, OSPF, VLANs, ACLs, NAT, NTP, AAA, SNMP
- **Interfaces** — IP addresses, descriptions, link types
- **Hostname** — for the config filename

### Step 2: Verify Syntax

Call `damira_search_vendor_docs` to verify platform-specific CLI syntax for any feature you're not 100% certain about. Pay attention to:
- Version-specific syntax differences (IOS vs IOS-XE vs NX-OS)
- Feature availability on the specific hardware platform
- Default behaviors that differ between versions

### Step 3: Generate Config

Write a complete, deployable configuration:
- Include `hostname`, management, AAA, NTP, logging, SNMP baseline
- Include all requested features with correct syntax
- Add comments (`!` for Cisco, `#` for Juniper/Arista) explaining each section
- Follow vendor best practices (use `enable secret` not `enable password`, use SNMPv3, etc.)

### Step 4: Save to Workspace

Save the config file to `configs/{hostname}.cfg`

Example filenames:
- `configs/chi-rtr-01.cfg`
- `configs/nyc-sw-core-01.cfg`
- `configs/fw-dmz-01.conf`

### Step 5: Verify

After saving, briefly summarize:
- What was configured
- Any assumptions made
- Recommended pre-deployment checks
