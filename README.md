---
title: IP Routing Lab with ACL Security Enhancement
description: Hands-on Cisco Packet Tracer tutorial for beginners in cybersecurity networking.
---

# IP Routing Fundamentals & ACL Security in Cisco Packet Tracer

![Lab Banner](images/topology.png)
*Network Topology: 3-router setup with OSPF for dynamic routing. (Screenshot from Packet Tracer)*

As a cybersecurity researcher, mastering IP Routing is essential—attackers exploit misrouted traffic for pivots. This lab builds a multi-site network, configures static/dynamic routing, then secures it with Access Control Lists (ACLs) to block unauthorized subnets. 

**Lab Time:** 1-2 hours  
**Tools:** Cisco Packet Tracer (free download from Cisco Networking Academy)  
**Security Focus:** Prevent lateral movement via route filtering.  
**Download:** [routing_lab.pkt](labs/routing_lab.pkt) (Upload your .pkt file to a `labs/` folder for sharing.)

## Key Concepts
- **IP Routing:** Directs packets between subnets using routing tables (static: manual; dynamic: protocols like OSPF).
- **ACLs:** Firewall-like filters on routers—permit/deny based on IP, protocol, ports.
- **Cyber Tie-In:** Blocks spoofed traffic from rogue subnets (e.g., 172.16.1.0/24).

| Component | Purpose | Security Risk if Misconfigured |
|-----------|---------|--------------------------------|
| Static Routing | Simple paths | No auto-updates; leaks via recon (e.g., Nmap). |
| OSPF | Dynamic updates | Route poisoning attacks. |
| Extended ACL | Granular blocking | Implicit deny can lock out legit users. |

## Hands-On Lab: Basic IP Routing

### Step 1: Build Topology
1. Open Packet Tracer > New project.
2. Drag: 3x 2911 Routers (Router1, Router2, Router3), 2x PCs (PC1, PC2), 2x Switches.
3. Connect: PC1 → Switch1 → Router1 Gig0/0; Router1 Gig0/1 → Router2 Gig0/0; Router2 Gig0/1 → Router3 Gig0/0; Router3 Gig0/1 → Switch2 → PC2.
   - Use Copper Straight-Through cables.

![Topology Screenshot](images/topology.png)
*Your built network—ensure all links are green.*

### Step 2: Assign IP Addresses
Click devices > CLI or Config tab.

**PC1:** IP: 192.168.1.10/24, Gateway: 192.168.1.1  
**Router1:**  
