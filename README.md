# CMPG325-2026-054 — Thari Restaurant Group (Vryburg)

**Student:** MASWANGANYE, TP (42041848)  
**Project ID:** CMPG325-2026-054  
**Client ID:** CLI-054  
**Networking Challenge:** IPv6 Dual-Stack Addressing & Routing  
**Addressing Block:** 10.26.0.0/16

## Project Overview

This project involves designing, simulating, and implementing a computer network for Thari Restaurant Group (Vryburg) using Cisco Packet Tracer. The network must support dual-stack IPv4 and IPv6, maintain logical separation between two departments, and accommodate a 25% user growth without renumbering (CR5).

## Milestone 1 Deliverables

- [x] Client requirements documented
- [x] Physical topology designed
- [x] Logical topology designed
- [x] IP addressing plan completed (IPv4 & IPv6)
- [x] GitHub repository initialised

## Key Design Decisions

| Decision | Justification |
| :--- | :--- |
| Logical Separation | VLANs (VLAN 10 for Admin, VLAN 20 for Service) |
| Routing Method | Router-on-a-Stick with sub-interfaces |
| IPv4 Addressing | /24 subnets for each VLAN to accommodate 25% growth |
| IPv6 Addressing | /64 subnets using 2001:db8::/32 documentation prefix |
| Networking Challenge | Dual-stack on all routers and end devices |

## Repository Contents

| Folder | Contents |
| :--- | :--- |
| `/docs` | Project documentation and diagrams |
| `/packet-tracer` | Cisco Packet Tracer `.pkt` file |
| `/configurations` | Router and switch configuration scripts |
| `/screenshots` | Evidence and verification screenshots |

## Author

- **Name:** TP MASWANGANYE
- **Student Number:** 42041848
- **Project:** CMPG325-2026-054
- **Date:** August 2026

## Academic Integrity

This work is submitted in accordance with the NWU Academic Integrity Policy. All work is my own and has been completed with reference to the CMPG325 Project Handbook.
