# Inter-VLAN Routing (Router-on-a-Stick) - Cisco Packet Tracer Lab

A Packet Tracer lab that splits a small network into four VLANs and routes between them using a Cisco 2911 router with subinterfaces (802.1Q trunking).

## Topology

- 1 x Cisco 2911 router
- 2 x Cisco 2960-24TT switches (Switch1, Switch2)
- 8 PCs (2 per VLAN)
- Each switch connects to the router over a trunk link

## VLAN and IP Plan

| VLAN | Name    | Subnet          | Gateway      | Hosts              |
|------|---------|-----------------|--------------|--------------------|
| 10   | SALES   | 192.168.10.0/29 | 192.168.10.1 | PC1 (.2), PC2 (.3) |
| 20   | HR      | 192.168.20.0/29 | 192.168.20.1 | PC3 (.2), PC4 (.3) |
| 30   | FINANCE | 192.168.30.0/29 | 192.168.30.1 | PC5 (.2), PC6 (.3) |
| 40   | IT      | 192.168.40.0/29 | 192.168.40.1 | PC7 (.2), PC8 (.3) |

Subnet mask on all hosts: 255.255.255.248 (/29)

## Router Subinterfaces

| Subinterface | VLAN | IP Address   |
|--------------|------|--------------|
| Gi0/0.10     | 10   | 192.168.10.1 |
| Gi0/0.20     | 20   | 192.168.20.1 |
| Gi0/1.30     | 30   | 192.168.30.1 |
| Gi0/1.40     | 40   | 192.168.40.1 |

## Verification

- `show ip interface brief` on the router shows all subinterfaces up/up
- Pings work within each VLAN (for example PC7 to PC8)
- Pings work between VLANs (for example PC3 to PC5, PC7 to PC1)
- TTL=127 on inter-VLAN replies shows the traffic passed through the router
- The first ping sometimes times out because of ARP; the rest succeed

## Repository Contents

- `lab/` - the Packet Tracer (.pkt) file
- `configs/` - router and switch running-configs
- `screenshots/` - topology, IP settings, and ping tests

## How to Run

1. Install Cisco Packet Tracer.
2. Open the .pkt file in the `lab/` folder.
3. Open any PC, go to Desktop, then Command Prompt, and ping across VLANs.

## What I Learned

- Creating VLANs and assigning access ports
- Configuring 802.1Q trunks
- Router-on-a-stick with subinterfaces
- Troubleshooting with ping and show ip interface brief
