# MPLS L3VPN Lab

This repository documents a full MPLS Layer 3 VPN (L3VPN) deployment using Juniper as the provider backbone and Cisco as the customer edge.  
It is meant as an educational reference for learning and practicing MPLS L3VPN end to end.

---

## Concepts Covered
This lab demonstrates the following technologies in sequence:

1. ISIS as the IGP in the provider backbone  
2. MPLS forwarding with LDP  
3. MP-BGP for VPNv4 address families  
4. VRFs for multiple customers (Cust1 and Cust2)  
5. OSPF PE–CE routing  
6. OSPF Sham Link to fix multi-site routing issues  

---

## Topology

<p align="center">
  <img src="topology/MPLS-L3VPN.png" width="600" alt="MPLS L3VPN Topology">
</p>

---

## Devices

Provider Backbone (Juniper JunOS):  
- PE1  
- PE2  
- P1  
- P2  

Customer Edge (Cisco IOS):  
- CE1-R1  
- CE1-R2  
- CE2-R1  
- CE2-R2  

---

## Repository Structure
mpls-l3vpn-lab/
│── README.md
│── topology/
│ ├── MPLS-L3VPN.png
│ ├── topology-diagram.drawio
│── configs/
│ ├── provider/
│ │ ├── PE1.conf
│ │ ├── PE2.conf
│ │ ├── P1.conf
│ │ ├── P2.conf
│ ├── customer/
│ │ ├── CE1-R1.conf
│ │ ├── CE1-R2.conf
│ │ ├── CE2-R1.conf
│ │ ├── CE2-R2.conf
│── notes/
│ ├── isis.md
│ ├── mpls-ldp.md
│ ├── mp-bgp.md
│ ├── vrf.md
│ ├── ospf-pe-ce.md
│ ├── sham-link.md
