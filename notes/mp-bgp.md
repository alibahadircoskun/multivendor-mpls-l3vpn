# MP-BGP (Multiprotocol BGP)

## Overview

Multiprotocol BGP (MP-BGP) extends regular BGP to support multiple address families beyond IPv4 unicast.
This is the control plane that makes MPLS VPNs possible. It allows PE routers to exchange customer routes while keeping them separated using VPN labels.

## Why MP-BGP?

* Standard BGP only carries IPv4 unicast routes.
* Data centers and service providers need to carry VPN routes, IPv6, multicast, and more.
* MP-BGP introduces new AFI/SAFI (Address Family Identifier / Subsequent Address Family Identifier) values to carry different types of routes.

In MPLS Layer 3 VPNs:

* PE routers use MP-BGP to advertise VPNv4 routes (IPv4 + Route Distinguisher).
* These routes include a label that tells the remote PE how to forward packets into the correct VRF.
* The SP core routers (P routers) don’t run MP-BGP. They only swap MPLS labels.

## Key Concepts

* **VPNv4 Address Family**: IPv4 routes with a Route Distinguisher (RD). Makes customer prefixes globally unique.
* **Route Target (RT)**: A BGP extended community that controls VPN membership (which VRFs import/export a route).
* **Label Binding**: BGP carries a label with each VPN route, used for forwarding.
* **IBGP**: MP-BGP is usually run as an IBGP session between all PE routers (directly or via route reflectors).

## Example Configuration (Juniper PE)

```shell
set protocols bgp group INT type internal
set protocols bgp group INT local-address 2.2.2.2
set protocols bgp group INT family inet-vpn unicast
set protocols bgp group INT export NHS
set protocols bgp group INT neighbor 22.22.22.22
```

Explanation:

* `family inet-vpn unicast` enables MP-BGP VPNv4.
* `export NHS` sets next-hop self for reflected routes.
* Neighbor is another PE (or route reflector).

## Example Configuration (Cisco PE)

```shell
router bgp 65530
 bgp log-neighbor-changes
 neighbor 22.22.22.22 remote-as 65530
 !
 address-family vpnv4
  neighbor 22.22.22.22 activate
  neighbor 22.22.22.22 send-community extended
 exit-address-family
```

## Real-World Usage

* ISPs and carriers universally use MP-BGP to deliver MPLS L3VPN services.
* Enterprises typically don’t run MP-BGP internally, but may interact with it indirectly when buying VPN services.
* MP-BGP can also be used in EVPN-VXLAN for data centers, where it carries MAC/IP routes.
