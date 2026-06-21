# Damira AI — Network Engineering Plugin for Cursor

CCIE-level network engineering tools inside Cursor. Troubleshoot, plan upgrades, audit configs, generate Ansible playbooks, and build lab topologies — all from Composer.

## Install

1. Install from the Cursor Marketplace (search "Damira AI")
2. Set your API key: `export DAMIRA_API_KEY="oncall_sk_your_key_here"`
3. Get a key at [damiraai.com/dashboard/api-keys](https://damiraai.com/dashboard/api-keys)

## Skills (Slash Commands)

| Command | What It Does |
|---------|-------------|
| `/troubleshoot` | GIDRP-methodology diagnosis with vendor-specific CLI commands |
| `/upgrade-plan` | Structured upgrade assessment → CVE check → MOP generation |
| `/config-audit` | Security and best practice audit (works with @file references) |
| `/generate-config` | Generate device configs saved to `configs/` |
| `/generate-playbook` | Generate Ansible playbooks saved to `playbooks/` |
| `/generate-lab` | Generate ContainerLab topologies saved to `labs/` |

## MCP Tools (15)

Bundled MCP server provides live network tools and domain expertise:

**Local tools** (run on your machine): ping, traceroute, port check, DNS lookup, config audit, connectivity diagnostic

**Domain expertise** (call Damira API): vendor doc search, CVE lookup, release notes, troubleshooting, upgrade planning, document templates

## How It Works

**Damira** provides CCIE-level domain data — vendor docs, CVE, troubleshooting diagnosis, upgrade assessments.

**Cursor** writes all outputs — config files, Ansible playbooks, Python scripts, MOPs, runbooks. Your AI model (built-in, DeepSeek BYOK, or Claude) handles the writing. Damira provides the network expertise.

## Cost

| Setup | Monthly |
|-------|---------|
| Cursor + Damira Pro | $40/mo |
| Cursor + DeepSeek BYOK + Damira | ~$32/mo |

Compare: SolarWinds ($10K+/yr), NetBrain ($15K+/yr)

## Supported Vendors

Cisco (IOS, IOS-XE, NX-OS, CUCM, ISE) · Juniper (Junos) · Arista (EOS) · Palo Alto (PAN-OS) · Fortinet (FortiOS) · Nokia (SR Linux)

## Links

- [Damira AI](https://damiraai.com)
- [Documentation](https://damiraai.com/docs)
- [GitHub](https://github.com/ciscoittech/damiraAI)
