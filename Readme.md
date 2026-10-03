# Testing Evidence – Milestone 2

|---|---|---|---|---|---|---|
| T1 | IPv4 intra-VLAN | PC-Admin1 | ping 10.26.10.3 | 0% loss | PASS | 04 |
| T2 | IPv4 inter-VLAN | PC-Admin1 | ping 10.26.20.2 | 0% loss | PASS | 04 |
| T3 | IPv6 intra-VLAN | PC-Admin1 | ping 2001:db8:10::3 | 0% loss | PASS | 05 |
| T4 | IPv6 inter-VLAN | PC-Admin1 | ping 2001:db8:20::2 | 0% loss | PASS | 05 |
| T5 | Reverse IPv4 | PC-Service1 | ping 10.26.10.2 | 0% loss | PASS | — |
| T6 | Reverse IPv6 | PC-Service1 | ping 2001:db8:10::2 | 0% loss | PASS | — |
| T7 | IPv4 traceroute | PC-Admin1 | tracert 10.26.20.2 | Via 10.26.10.1 | PASS | — |
| T8 | IPv6 traceroute | PC-Admin1 | tracert 2001:db8:20::2 | Via 2001:db8:10::1 | PASS | — |
| T9 | R1 IPv6 interfaces | R1 | show ipv6 interface brief | Both up/up | PASS | 07 |
| T10 | VLAN verification | S1 | show vlan brief | VLANs 10 & 20 active | PASS | 06 |
| T11 | CR5 growth | PC-Admin4 | ping 10.26.20.5 | Success | PASS | — |
