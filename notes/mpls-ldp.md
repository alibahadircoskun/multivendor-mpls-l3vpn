# MPLS with LDP

## What is MPLS?

Multiprotocol Label Switching (MPLS) is a forwarding technology where packets are forwarded based on short labels instead of long IP lookups. It enables faster forwarding and allows advanced services like VPNs and traffic engineering.

## What is LDP?

Label Distribution Protocol (LDP) is used to distribute MPLS labels between routers. LDP establishes label mappings for each prefix in the IGP (OSPF or IS-IS), creating a Label Switched Path (LSP) across the provider core.

## How it works

1. The IGP (OSPF/IS-IS) provides reachability information.
2. LDP runs between routers and assigns a label to each IGP prefix.
3. Routers exchange these labels with neighbors.
4. Forwarding tables are updated so packets can be switched using labels.

## Why MPLS + LDP?

* Simplifies MPLS deployment by automatically assigning labels to all IGP routes.
* Works well for L3VPNs and L2VPNs.
* Requires little manual configuration beyond enabling LDP on interfaces.

## Example (Juniper)

```bash
set protocols ldp interface all
```

This enables LDP on all interfaces where IGP is running, ensuring that MPLS labels are exchanged across the provider core.

## Example (Cisco IOS)

```bash
mpls ip
mpls label protocol ldp
interface GigabitEthernet0/0
  mpls ip
```

## Real-world usage today

* **Still used:** Many ISPs and enterprises continue to use LDP for MPLS VPN services because it’s simple and proven.
* **Declining:** Larger service providers are moving toward Segment Routing (SR-MPLS or SRv6), which eliminates the need for LDP and simplifies the control plane.
* **Why still learn LDP?** It remains common in production, and understanding it provides a foundation for learning why Segment Routing was developed.
