# OSPF Between PE and CE

## Overview

OSPF can be used as the routing protocol between Provider Edge (PE) routers and Customer Edge (CE) routers. This allows dynamic route exchange between the customer's network and the provider's VRF.

## How it works

* Each CE router runs OSPF and advertises its routes into the PE.
* The PE router runs OSPF within the VRF and imports these routes into the VRF routing table.
* Optionally, the PE router can redistribute VRF routes into MP-BGP to advertise them to other PE routers.

## Juniper Example

```bash
set routing-instances Customer1 protocols ospf area 0.0.0.0 interface ge-0/0/1.0
set routing-instances Customer1 protocols ospf area 0.0.0.0 interface lo0.1
```

Explanation:

* Interfaces ge-0/0/1.0 and lo0.1 participate in OSPF for Customer1 VRF.
* OSPF routes from CE are learned dynamically and installed in the VRF.

## Cisco Example

```shell
router ospf 1
 network 192.168.11.0 0.0.0.255 area 0
```

* This runs OSPF on CE interfaces that connect to the PE.

## Considerations

* Using OSPF between PE and CE is not common in modern service provider networks.
* Often, static routes or BGP are used between PE and CE instead.
* Dynamic OSPF may be used for legacy deployments or when customers require it.
* PE-CE OSPF is usually limited to a single area and simple topologies.

## Lab Usage

* In this lab, OSPF is used to simulate customer networks and dynamically distribute customer prefixes into the PE VRF.
* The lab shows how a sham-link may be required when customers have multiple sites connected to different PEs.
