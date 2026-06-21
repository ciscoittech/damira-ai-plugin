---
name: generate-lab
description: Generate a ContainerLab topology for lab testing. Use when the user asks to create a lab, test topology, simulate a network, or build a practice environment for BGP, OSPF, MPLS, EVPN, or any protocol.
---

# ContainerLab Topology Generation

Generate complete ContainerLab topologies with startup configs for network lab testing.

## Workflow

### Step 1: Gather Requirements

Ask the user for:
- **Purpose** — what to test (e.g., BGP convergence, OSPF multi-area, MPLS L3VPN, EVPN-VXLAN)
- **Nodes** — how many and what roles (e.g., 2 spine + 4 leaf, 3 routers + 1 firewall)
- **Node types** — container images:
  - `ceos` — Arista cEOS (requires image)
  - `crpd` — Juniper cRPD (requires image)
  - `srl` — Nokia SR Linux (free, no license)
  - `frr` — FRRouting on Linux (free)
  - `linux` — Alpine Linux hosts
  - `vyos` — VyOS router (free)
- **Connections** — topology type (full mesh, leaf-spine, hub-spoke, ring)

### Step 2: Generate Topology

Create a ContainerLab YAML topology file:
- Use proper `topology:` structure with `nodes:` and `links:`
- Set `kind:` and `image:` for each node
- Define `startup-config:` pointing to config files
- Set management network if needed

### Step 3: Generate Startup Configs

For each node, generate a startup configuration:
- Interfaces with IP addressing matching the topology links
- Routing protocol configuration matching the lab purpose
- Loopback interfaces for router-IDs
- Use the correct syntax for each platform (FRR uses `frr.conf`, SR Linux uses YAML/JSON)

### Step 4: Save to Workspace

Save files:
- Topology: `labs/{lab-name}.yml`
- Configs: `labs/configs/{node-name}.cfg` (one per node)
- README: `labs/{lab-name}-README.md`

### Step 5: Provide Deploy Instructions

Include in the README:
```bash
# Deploy the lab
cd labs/
sudo clab deploy -t {lab-name}.yml

# Check status
sudo clab inspect -t {lab-name}.yml

# Connect to a node
ssh admin@clab-{lab-name}-{node-name}

# Destroy when done
sudo clab destroy -t {lab-name}.yml
```

### Step 6: Verification Commands

Include verification commands in the README specific to the lab purpose:
- BGP lab: `show ip bgp summary`, `show ip bgp`
- OSPF lab: `show ip ospf neighbor`, `show ip ospf database`
- MPLS lab: `show mpls ldp neighbor`, `show mpls forwarding-table`
