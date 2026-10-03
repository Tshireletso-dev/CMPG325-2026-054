# Testing Evidence – Milestone 2
# CMPG325 Project – CLI-2026-054
## Thai Restaurant Group (Vryburg)

# Student Information
- **Name:** MASWANGANYE, TP
- **Student Number:** 42041848
- **Project ID:** CMPG325 Project
- **Client ID:** CLI-2026-054

### Organisation
Thai Restaurant Group (Vryburg) – Hospitality Industry

### Assigned Networking Challenge
IPv6 Dual-Stack Addressing & Routing

### Addressing Block
`10.26.0.0/16`

### Design Constraint
Two departments share a physical floor but must remain logically separated (VLANs).

### Change Request (CR5)
User numbers grow by 25% — addressing plan must absorb this **without renumbering**.

---

## 1. Project Overview

This project designs and simulates a computer network for the Thai Restaurant Group (Vryburg). The network provides:

- Logical separation between two departments using **VLANs**
- **Inter-VLAN routing** using the Router-on-a-Stick method
- **IPv6 dual-stack** addressing and routing (both IPv4 and IPv6 operational)
- A scalable addressing plan that handles a 25% growth without renumbering

---

## 2. Physical Topology

### 2.1 Device Inventory

| Device | Model | Quantity | Role |
|---|---|---|---|
| R1 | Cisco 2911 | 1 | Inter-VLAN routing + dual-stack gateway |
| S1 | Cisco 2960-24TT | 1 | Access layer switching + VLAN segmentation |
| PC-Admin1–3 | PC-PT | 3 | Administration Department (VLAN 10) |
| PC-Service1–3 | PC-PT | 3 | Service/Kitchen Department (VLAN 20) |

### 2.2 Physical Connections

| Device 1 | Interface | Device 2 | Interface | Cable |
|---|---|---|---|---|
| R1 | Gig0/0 | S1 | Gig0/1 | Copper Straight-Through |
| PC-Admin1 | Fa0 | S1 | Fa0/1 | Copper Straight-Through |
| PC-Admin2 | Fa0 | S1 | Fa0/2 | Copper Straight-Through |
| PC-Admin3 | Fa0 | S1 | Fa0/3 | Copper Straight-Through |
| PC-Service1 | Fa0 | S1 | Fa0/4 | Copper Straight-Through |
| PC-Service2 | Fa0 | S1 | Fa0/5 | Copper Straight-Through |
| PC-Service3 | Fa0 | S1 | Fa0/6 | Copper Straight-Through |

---

## 3. Logical Topology

### 3.1 Design Decisions

| Decision | Justification |
|---|---|
| VLAN Segmentation | Logical separation between departments on the same floor |
| Router-on-a-Stick | Cost-effective inter-VLAN routing on a single router interface |
| Dual-Stack | Meets the assigned IPv6 dual-stack networking challenge |
| /24 IPv4 Subnets | Absorbs 25% growth without renumbering |
| /64 IPv6 Prefixes | Future-proof — over 18 quintillion addresses per subnet |

### 3.2 VLAN Assignment

| VLAN ID | VLAN Name | Department | IPv4 Subnet | IPv6 Prefix |
|---|---|---|---|---|
| 10 | Administration | Admin Staff | 10.26.10.0/24 | 2001:db8:10::/64 |
| 20 | Service | Kitchen/Service Staff | 10.26.20.0/24 | 2001:db8:20::/64 |

---

## 4. IP Addressing Plan

### 4.1 IPv4 Addressing Plan

| Department | VLAN | Subnet | Mask | CIDR | Usable Hosts | Gateway |
|---|---|---|---|---|---|---|
| Administration | 10 | 10.26.10.0 | 255.255.255.0 | /24 | 254 | 10.26.10.1 |
| Service / Kitchen | 20 | 10.26.20.0 | 255.255.255.0 | /24 | 254 | 10.26.20.1 |
| Reserved Future | — | 10.26.30.0 | 255.255.255.0 | /24 | 254 | 10.26.30.1 |
| Reserved Future | — | 10.26.40.0 | 255.255.255.0 | /24 | 254 | 10.26.40.1 |

### 4.2 IPv6 Addressing Plan (using documentation prefix `2001:db8::/32`)

| Department | VLAN | IPv6 Prefix | Gateway |
|---|---|---|---|
| Administration | 10 | 2001:db8:10::/64 | 2001:db8:10::1 |
| Service / Kitchen | 20 | 2001:db8:20::/64 | 2001:db8:20::1 |

### 4.3 Device IP Assignments

| Device | VLAN | IPv4 Address | Gateway | IPv6 Address |
|---|---|---|---|---|
| R1 (Sub-interface .10) | 10 | 10.26.10.1/24 | — | 2001:db8:10::1 |
| R1 (Sub-interface .20) | 20 | 10.26.20.1/24 | — | 2001:db8:20::1 |
| PC-Admin1 | 10 | 10.26.10.2/24 | 10.26.10.1 | 2001:db8:10::2 |
| PC-Admin2 | 10 | 10.26.10.3/24 | 10.26.10.1 | 2001:db8:10::3 |
| PC-Admin3 | 10 | 10.26.10.4/24 | 10.26.10.1 | 2001:db8:10::4 |
| PC-Service1 | 20 | 10.26.20.2/24 | 10.26.20.1 | 2001:db8:20::2 |
| PC-Service2 | 20 | 10.26.20.3/24 | 10.26.20.1 | 2001:db8:20::3 |
| PC-Service3 | 20 | 10.26.20.4/24 | 10.26.20.1 | 2001:db8:20::4 |

### 4.4 CR5 Growth Justification (25% Increase)

| Aspect | Justification |
|---|---|
| IPv4 Allocation | Each department has a /24 subnet (254 usable hosts). A 25% increase from 20 users needs only 25 addresses — well within 254. **No renumbering needed.** |
| Future Expansion | Reserved /24 subnets (10.26.30.0/24, 10.26.40.0/24) available for future expansion |
| IPv6 Allocation | /64 prefix provides over 18 quintillion addresses — renumbering is unnecessary for the foreseeable future |

---

## 5. Configurations

Configuration files are stored in the `/configs` folder:

- `R1-running-config.txt` — Router R1 full running configuration
- `S1-running-config.txt` — Switch S1 full running configuration

### 5.1 Key R1 Configuration Highlights

```cisco
ipv6 unicast-routing

interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.26.10.1 255.255.255.0
 ipv6 address 2001:db8:10::1/64

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.26.20.1 255.255.255.0
 ipv6 address 2001:db8:20::1/64
