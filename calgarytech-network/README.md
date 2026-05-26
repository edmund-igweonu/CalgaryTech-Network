# Calgary Technology Services - Enterprise Campus Network

## Overview
This is a production-ready enterprise network design demonstrating CCNA-level concepts for a medium-sized organization with 300+ users across multiple buildings and a remote branch office.

## Network Features
- **VLANs:** 10 segments (departments, servers, guest, IoT)
- **Inter-VLAN Routing:** Layer 3 switching on core
- **DHCP:** Centralized IP assignment
- **Security:** ACLs for guest isolation and finance restrictions
- **NAT/PAT:** Single public IP for internet access
- **WAN:** Serial link to branch office
- **Redundancy:** Dual distribution switches (can expand to dual core)
- **Port Security:** MAC address limits on access switches

## Quick Start
1. Open `CalgaryTech-Network.pkt` in Packet Tracer
2. Review IP addressing scheme (see IP_SCHEME.md)
3. Test connectivity using testing procedures (see TESTING.md)
4. Review device configs in `/configs` folder

## Directory Structure
├── CalgaryTech-Network.pkt       # Packet Tracer file
├── README.md                      # This file
├── IP_SCHEME.md                   # Complete addressing plan
├── TESTING.md                     # Test procedures
├── TOPOLOGY.png                   # Network diagram
└── configs/
├── Core-1.txt
├── R1-Edge.txt
├── Dist-SW1.txt
└── ... (all device configs)

## Credentials
- **Enable Secret:** cisco123 / dist123 / access123 (varies by device)
- **Console:** console123
- **VTY:** vty123

## Author: Edmund Igweonu
Network Engineer Candidate - Calgary, AB
Designed for CCNA demonstration and enterprise deployment scenarios
