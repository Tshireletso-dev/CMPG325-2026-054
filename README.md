# CMPG 325 — Thari Restaurant Group Network Design

**Student:** [Your Full Name]
**Student Number:** [Your Number]
**Module:** CMPG 325 — Computer Networks
**Project Period:** 14 August – 16 October 2026
**Client:** Thari Restaurant Group (Vryburg)
**Industry:** Hospitality
**Assigned Feature:** IPv6 Dual-Stack Addressing & Routing
**IPv4 Block:** 10.26.0.0/16
**IPv6 Site Prefix:** 2001:db8:26::/48

---

## 1. Project Overview

This portfolio documents the design, implementation, testing, and reflection of a dual-stack (IPv4 + IPv6) network for Thari Restaurant Group. Two departments sharing a floor are logically separated using VLANs, subnets, and ACLs on both protocol stacks.

## 2. The Client Problem

Thari Restaurant Group operates a head office in Vryburg with two departments sharing a single floor:

- **Front-of-House (Reservations)** — guest-facing staff
- **Back-of-House (Finance & Admin)** — restricted data

The client requires:
- Logical separation between the two departments
- Support for both IPv4 and IPv6 (dual-stack)
- An addressing plan that absorbs 25% user growth (CR5) without renumbering

## 3. Repository Structure

| Folder | Contents |
|---|---|
| `/pkt` | Packet Tracer project file |
| `/configs` | Running configs from R1 and Switch0 |
| `/docs` | Technical report and addressing tables |
| `/screenshots` | Evidence of configuration and testing |
| `/tests` | Test plan and results |
| `/reflections` | Personal reflection on the project |

## 4. Design Summary

### Topology
- 1 × Router (R1) — dual-stack, router-on-a-stick
- 1 × Switch (2960) — VLAN trunking
- 8 × PCs — split across VLAN 10 and VLAN 20

### VLANs

| VLAN | Name | Purpose |
|---|---|---|
| 10 | ADMIN | Front-of-House |
| 20 | SERVICE | Back-of-House |

### IPv4 Addressing

| VLAN | Subnet | Gateway |
|---|---|---|
| 10 | 10.26.0.0/22 | 10.26.0.1 |
| 20 | 10.26.4.0/22 | 10.26.4.1 |

### IPv6 Addressing

| VLAN | Prefix | Gateway |
|---|---|---|
| 10 | 2001:db8:26:10::/64 | 2001:db8:26:10::1 |
| 20 | 2001:db8:26:20::/64 | 2001:db8:26:20::1 |

## 5. Key Features Implemented

- [x] VLAN segmentation (VLAN 10, 20)
- [x] 802.1Q trunking between switch and router
- [x] Router-on-a-stick inter-VLAN routing
- [x] IPv4 addressing per the plan
- [x] IPv6 dual-stack addressing
- [x] `ipv6 unicast-routing` enabled
- [x] OSPFv2 (IPv4 dynamic routing)
- [x] OSPFv3 (IPv6 dynamic routing)
- [x] IPv4 ACL — block Service → Admin
- [x] IPv6 ACL — block Service → Admin
- [ ] DHCP server (pending)
- [ ] ISP router / WAN link (pending)

## 6. Change Request CR5 — Growth Analysis

| VLAN | Current Users | +25% | Subnet Capacity | Headroom |
|---|---|---|---|---|
| 10 | 60 | 75 | 1022 | 947 free |
| 20 | 40 | 50 | 1022 | 972 free |

**Conclusion:** The /22 IPv4 subnets and /64 IPv6 prefixes absorb the 25% growth without any renumbering. Gateways, masks, and routing advertisements remain unchanged.

## 7. Evidence Index

| Evidence | Location |
|---|---|
| Packet Tracer file | `/pkt/` |
| Router running config | `/configs/R1-running-config.txt` |
| Switch running config | `/configs/Switch0-running-config.txt` |
| Technical report | `/docs/technical-report.md` |
| Screenshots | `/screenshots/` |
| Test plan and results | `/tests/` |
| Reflection | `/reflections/reflection.md` |

## 8. Video Demonstration

INSET video (15–20 minutes): [PASTE YOUTUBE OR DRIVE LINK HERE]

## 9. References

- Cisco IOS IPv6 Configuration Guide
- RFC 4291 — IP Version 6 Addressing Architecture
- RFC 4861 — Neighbor Discovery for IPv6
- RFC 5340 — OSPF for IPv6

## 10. Declaration

I declare that this portfolio is my own work, except where acknowledged.



