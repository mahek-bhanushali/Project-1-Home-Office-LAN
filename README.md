\# Home/Small-Office LAN (Cisco Packet Tracer)



\## Overview

A small office network with two LAN segments, a central server providing

DHCP, DNS and HTTP, and a router connecting both subnets.



\## Topology

!\[Topology](screenshots/topology.png)



\## IP Addressing

| Segment | Subnet | Gateway | Devices |

|---------|--------|---------|---------|

| LAN 1 | 192.168.1.0/24 | 192.168.1.1 | 2 PCs, Server (192.168.1.5) |

| LAN 2 | 192.168.2.0/24 | 192.168.2.1 | 2 PCs |



\## Services Configured

\- \*\*DHCP:\*\* Two pools (LAN1, LAN2) delivering IP, mask, gateway and DNS.

&#x20; `ip helper-address` on the router relays LAN 2 requests to the server.

\- \*\*DNS:\*\* A record `www.office.com -> 192.168.1.5`

\- \*\*HTTP:\*\* Internal web server hosted on the same server.



\## Tests and What They Proved

| Test | Result | What it proves |

|------|--------|----------------|

| `ipconfig /all` on PCs | IP, gateway, DNS received | DHCP works for both LANs |

| `ping 192.168.1.1` | Success | PC reaches its gateway |

| `ping` PC in other LAN | Success | Inter-subnet routing works |

| Browse `www.office.com` | Page loads | DNS resolution and HTTP work end to end |



\## Issues Faced and Fixes

\- Switch 1 PCs received only IP and mask: a duplicate DHCP pool for the

&#x20; same subnet with empty gateway/DNS was being used. Removed it so each

&#x20; subnet has exactly one pool.

\- LAN 2 clients could not get an address until the `ip helper-address`

&#x20; was added, because DHCP discovery is a broadcast and routers don't forward it.



\## Tools

Cisco Packet Tracer



\## Files

\- `Small-office-project.pkt`: open in Packet Tracer

\- `router-config.txt`: router running config

