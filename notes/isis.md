# IS-IS (Intermediate System to Intermediate System)

IS-IS is a link-state Interior Gateway Protocol (IGP) often used in service provider networks. It is well-suited for large topologies and supports both IPv4 and IPv6. Unlike OSPF, IS-IS runs directly over Layer 2 (CLNP), not IP, which makes it protocol-independent.

## Key Concepts

- **IS (Intermediate System):** A router running IS-IS.
- **ES (End System):** A host (non-router) in IS-IS terminology.
- **Level-1 (L1):** Intra-area routing (like OSPF area).
- **Level-2 (L2):** Inter-area routing, backbone of IS-IS.
- **L1/L2 routers:** Participate in both levels; act as area border routers.
- **NSAP / NET (Network Entity Title):** Router identifier in IS-IS.  
  Example format: `49.0000.0000.0000.0022.00`
  - `49` = private AFI
  - Middle = system ID (usually loopback IP in hex)
  - Last `.00` = NSEL (selector)

## Why IS-IS for Service Providers?

- Scales better than OSPF in large networks.
- Flexible addressing (not tied to IPv4).
- Runs over Layer 2, which simplifies operation in MPLS cores.
- Widely adopted in ISP backbones for IGP + MPLS underlay.

## Basic Juniper IS-IS Configuration

Enable IS-IS globally and on interfaces:

```bash
set protocols isis interface all
set interfaces lo0 unit 0 family iso address 49.0000.0000.0000.0022.00
