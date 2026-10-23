# Computer Networks Lab – Experiments Report

**Course:** 21CSC302J – Computer Networks (Semester V)  
**Name:** K.S. Yashvin Kumar  
**Register No.:** R2411030050007  
**Tool:** Cisco Packet Tracer

**Experiments covered**

1. Lab 1 – Introduction to Packet Tracer, Peer-to-Peer Communication, Study of Cables and Color Codes
2. Lab 3 – Router Configuration (Creating Passwords, Configuring Interfaces)

---

# Experiment 1: Introduction to Packet Tracer, Peer-to-Peer Communication, Study of Cables and Color Codes

## Aim
To get familiar with Cisco Packet Tracer, build a simple two-PC network, verify communication using ping, and study Ethernet cable types and their colour codes.

## Tools Used
Cisco Packet Tracer; 2 × PC-PT; 1 × Switch (2960); copper straight-through cables.

## Procedure
1. Launched Cisco Packet Tracer and explored the workspace, device selection panel and tools.
2. Placed two PCs (PC0, PC1) and one switch on the workspace.
3. Connected each PC to the switch with a **copper straight-through** cable.

   ![Topology](screenshots/exp1_01_topology.png)

4. Opened PC0 → Desktop → IP Configuration and set IP `192.168.1.1`, subnet mask `255.255.255.0`.

   ![PC0 IP configuration](screenshots/exp1_02_pc0_ip.png)

5. Opened PC1 → Desktop → IP Configuration and set IP `192.168.1.2`, subnet mask `255.255.255.0`.

   ![PC1 IP configuration](screenshots/exp1_03_pc1_ip.png)

6. On PC0, opened Desktop → Command Prompt and ran `ping 192.168.1.2`.

   ![Ping output](screenshots/exp1_04_ping.png)

7. Studied the cable types and colour codes (below).

## Cable Study

**Straight-through cable** – connects *different* devices (PC ↔ switch, router ↔ switch). Both ends use the same standard (T568B).

**Crossover cable** – connects *similar* devices (PC ↔ PC, switch ↔ switch, PC ↔ router). One end is T568A, the other is T568B.

| Pin | T568B (straight-through, both ends) | T568A (other end of crossover) |
|-----|-------------------------------------|--------------------------------|
| 1 | White/Orange | White/Green |
| 2 | Orange | Green |
| 3 | White/Green | White/Orange |
| 4 | Blue | Blue |
| 5 | White/Blue | White/Blue |
| 6 | Green | Orange |
| 7 | White/Brown | White/Brown |
| 8 | Brown | Brown |

## Output
PC0 received 4 replies from 192.168.1.2 (Sent = 4, Received = 4, Lost = 0, 0% loss), confirming peer-to-peer communication through the switch.

## Result
A two-PC network was built in Packet Tracer, both PCs were addressed in the 192.168.1.0/24 network, and connectivity was verified with ping. The straight-through and crossover cable colour codes were studied.

---

# Experiment 2: Router Configuration (Passwords and Interfaces)

## Aim
To configure console, enable and VTY passwords on a router, configure its interfaces, and verify connectivity between two networks through the router.

## Tools Used
Cisco Packet Tracer; 1 × Router (2911); 2 × PC-PT; copper cross-over cables.

## Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|--------|-----------|------------|-------------|-----------------|
| R1 | Gig0/1 | 192.168.1.1 | 255.255.255.0 | – |
| R1 | Gig0/2 | 192.168.2.1 | 255.255.255.0 | – |
| PC0 | NIC | 192.168.1.2 | 255.255.255.0 | 192.168.1.1 |
| PC1 | NIC | 192.168.2.2 | 255.255.255.0 | 192.168.2.1 |

## Procedure
1. Placed one router and two PCs on the workspace and connected PC0 → Gig0/1 and PC1 → Gig0/2 using copper cross-over cables.

   ![Topology](screenshots/exp2_01_topology.png)

2. Opened the router → CLI tab and entered privileged and global configuration mode: `enable`, `configure terminal`.
3. Set the console password: `line console 0`, `password cisco`, `login`.
4. Set the enable password: `enable password cisco`.
5. Set the VTY password: `line vty 0 4`, `password cisco`, `login`.

   ![Password configuration](screenshots/exp2_02_passwords.png)

6. Configured Gig0/1: `interface gigabitEthernet0/1`, `ip address 192.168.1.1 255.255.255.0`, `no shutdown`.
7. Configured Gig0/2: `interface gigabitEthernet0/2`, `ip address 192.168.2.1 255.255.255.0`, `no shutdown`.

   ![Interface configuration](screenshots/exp2_03_interfaces.png)

8. Verified with `show ip interface brief` (both interfaces up/up).

   ![show ip interface brief](screenshots/exp2_04_show_ip_int_brief.png)

9. Configured the PCs with the IP addresses and default gateways from the addressing table.

   ![PC0 IP configuration](screenshots/exp2_05_pc0_ip.png)
   ![PC1 IP configuration](screenshots/exp2_06_pc1_ip.png)

10. From PC0 ran `ping 192.168.2.2`.

    ![Ping output](screenshots/exp2_07_ping.png)

Full command listing: [`configs/lab3_router_config.txt`](configs/lab3_router_config.txt)

## Output
Ping from PC0 (192.168.1.2) to PC1 (192.168.2.2) succeeded through the router (the first packet may time out due to ARP).

## Result
The router passwords and interfaces were configured successfully and the two networks communicated through the router.

---

## Conclusion
Both experiments were completed in Cisco Packet Tracer: peer-to-peer communication through a switch with a study of cable colour codes, and router password and interface configuration with inter-network connectivity.

## Repository Layout
```
README.md          – this report
screenshots/       – screenshots used in the report
configs/           – router configuration commands
packet-tracer/     – .pkt files for both experiments
```
