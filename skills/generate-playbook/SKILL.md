---
name: generate-playbook
description: Generate an Ansible playbook for network automation. Use when the user asks to automate a network task, create a playbook, deploy changes across multiple devices, or build network automation.
---

# Ansible Playbook Generation

Generate production-ready Ansible playbooks for network automation.

## Workflow

### Step 1: Gather Requirements

Ask the user for:
- **Task** — what to automate (e.g., deploy VLANs, backup configs, upgrade firmware)
- **Target devices** — how many, what type (e.g., 3x Arista 7050X, 10x Cisco C9300)
- **Platform** — determines Ansible collection (cisco.ios, arista.eos, junipernetworks.junos)
- **Variables** — any parameters (VLAN IDs, interface names, IP ranges)

### Step 2: Verify Module Syntax

Call `damira_search_vendor_docs` to verify:
- Correct Ansible collection and module names for the platform
- Module parameters and syntax
- Any version-specific considerations

Use the correct collections:
- Cisco IOS/IOS-XE: `cisco.ios`
- Cisco NX-OS: `cisco.nxos`
- Arista EOS: `arista.eos`
- Juniper Junos: `junipernetworks.junos`
- Palo Alto: `paloaltonetworks.panos`
- Fortinet: `fortinet.fortios`

### Step 3: Generate Playbook

Write a complete playbook including:
- **Inventory file** — example hosts file with device groups
- **Group vars** — platform-specific connection settings (`ansible_network_os`, `ansible_connection`)
- **Playbook** — tasks with proper module usage, handlers, tags
- **Error handling** — `rescue` blocks for critical operations
- **Idempotency** — playbook should be safe to run multiple times

### Step 4: Save to Workspace

Save files:
- Playbook: `playbooks/{task-name}.yml`
- Inventory: `playbooks/inventory/{group-name}.yml` (if not existing)
- Group vars: `playbooks/group_vars/{group}.yml` (if needed)

### Step 5: Provide Run Instructions

Show the user how to run it:
```bash
ansible-playbook -i playbooks/inventory/hosts.yml playbooks/{task-name}.yml --check
# Review output, then run for real:
ansible-playbook -i playbooks/inventory/hosts.yml playbooks/{task-name}.yml
```

Include `--check` (dry run) before the actual run.
