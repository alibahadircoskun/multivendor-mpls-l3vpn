# VRF (Virtual Routing and Forwarding)

## Overview

VRF allows a single router to maintain multiple separate routing tables. This is essential in service provider networks to keep customer traffic isolated while using shared infrastructure.

## Key Concepts

* Each VRF has its own routing table.
* Route Distinguisher (RD) makes routes globally unique across all VRFs.
* Route Target (RT) defines which VRFs import or export specific routes.
* Interfaces are assigned to VRFs to isolate customer traffic.
* VRFs work with MP-BGP in MPLS L3VPN to transport customer routes across the provider core.

## Why VRFs are used

* Isolate customer networks on the same provider hardware.
* Allow overlapping IP addresses between different customers.
* Enable MPLS VPNs by combining with MP-BGP and MPLS labels.

## Basic Juniper VRF Configuration Example

```bash
set routing-instances Customer1 instance-type vrf
set routing-instances Customer1 interface ge-0/0/1.0
set routing-instances Customer1 route-distinguisher 1.1.1.1:1
set routing-instances Customer1 vrf-target target:65530:1
```

Explanation:

* Assign interface ge-0/0/1.0 to Customer1 VRF.
* RD ensures that Customer1 routes are unique in the VPN.
* VRF target controls import/export of routes for this VRF.

## Basic Cisco VRF Configuration Example

```shell
ip vrf Customer1
 rd 1.1.1.1:1
 route-target export 65530:1
 route-target import 65530:1
interface GigabitEthernet0/0
 vrf forwarding Customer1
 ip address 192.168.11.1 255.255.255.0
```

Explanation:

* Create VRF named Customer1.
* Assign RD and RT values.
* Associate the interface with the VRF.

## Usage in the Lab

* PE routers create a VRF for each customer.
* Interfaces connected to CE routers are assigned to the corresponding VRF.
* MP-BGP advertises routes from VRFs to other PE routers using VPNv4 routes and labels.
