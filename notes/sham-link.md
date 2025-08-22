# OSPF Sham Link

## Overview

A sham link is a logical OSPF connection between two PE routers in a multi-site VPN scenario. It is used to maintain OSPF routing over an MPLS Layer 3 VPN when the standard OSPF adjacency would otherwise appear to be across an external link.

## Why Sham Links Are Needed

* When a customer has multiple sites connected to different PE routers and OSPF is running between CE routers, the OSPF domain may see the MPLS VPN as an external link.
* This can cause OSPF to treat routes as external and prevent proper route propagation between areas.
* A sham link allows OSPF to treat the VPN path between PE routers as an intra-area link, preserving the correct OSPF metric and topology.

## Juniper Example

```bash
set routing-instances Customer1 protocols ospf sham-link local 111.111.111.111
set routing-instances Customer1 protocols ospf sham-link remote 222.222.222.222
```

Explanation:

* `local` is the IP address of the sham-link interface on the local PE.
* `remote` is the IP address of the sham-link on the remote PE.
* This creates a virtual OSPF link across the MPLS VPN, ensuring intra-area behavior.

## Cisco Example

```shell
router ospf 1 vrf Customer1
 area 0 sham-link 111.111.111.111 222.222.222.222
```

* Similar concept: the sham link logically connects two PE routers across the VPN.

## Considerations

* Sham links are specific to OSPF running over MPLS L3VPNs.
* Not needed if BGP is used as the CE-PE routing protocol.
* Useful in multi-site customer OSPF deployments where intra-area consistency must be maintained.

## Lab Usage

* In the lab, sham links are configured between PEs for Customer1 and Customer2.
* This ensures OSPF between CE sites behaves as if all CE routers are in the same area, despite being connected to different PE routers across the MPLS core.
