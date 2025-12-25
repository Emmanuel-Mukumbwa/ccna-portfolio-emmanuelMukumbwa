Project 1: VLAN & Inter-VLAN Routing with Router-on-a-Stick
By Emmanuel Mukumbwa | CCNA Certified Network Engineer

?? Project Summary
Complete implementation of VLAN segmentation across multiple switches with inter-VLAN routing via Router-on-a-Stick method. This project includes troubleshooting and resolution of real-world Native VLAN mismatch issues.

?? Project Statistics
Devices: 1 Router (2911), 2 Switches (2960), 6 PCs, 1 Server

VLANs Configured: 4 (Sales, Engineering, IT, Management)

Protocols: 802.1Q, DHCP, STP, CDP, ICMP

Testing: Full connectivity matrix validated

Issues Resolved: 1 (Native VLAN Mismatch)

Configuration Files: 3 (Router, Switch1, Switch2)

?? Skills Demonstrated
Core Networking
? VLAN Configuration & Management

? 802.1Q Trunking Implementation

? Inter-VLAN Routing (Router-on-a-Stick)

? DHCP Server Configuration

? Subinterface Configuration

Troubleshooting
? CDP Error Analysis

? Spanning Tree Protocol Issues

? Native VLAN Configuration

? Layer 2 Connectivity Problems

Professional Skills
? Configuration Documentation

? Problem-Solving Methodology

? Verification Testing

? Best Practices Implementation

?? Project Structure
text
01-vlan-intervlan-routing/
+-- config/
¦   +-- switch1-final-config.txt
¦   +-- switch2-final-config.txt
¦   +-- router-final-config.txt
+-- packet-tracer-files/
¦   +-- vlan-project-complete.pkt
+-- documentation/
¦   +-- project-overview.md
¦   +-- technical-specifications.md
¦   +-- troubleshooting-native-vlan-mismatch.md
+-- verification/
¦   +-- test-procedures.txt
¦   +-- verification-results.txt
+-- screenshots/
¦   +-- error-cdp-mismatch.png
¦   +-- spanning-tree-unblock.png
¦   +-- show-interfaces-trunk-before.png
¦   +-- show-interfaces-trunk-after.png
¦   +-- ping-tests-successful.png
+-- README.md (this file)
??? Technical Implementation
Network Design
text
[Router: 2911]----[SW1: 2960]----[SW2: 2960]
       Gi0/0/0          Fa0/24         Gi0/1
          |                |              |
     Subinterfaces    Access Ports   Access Ports
     (VLANs 10,20,    (PCs 1,2,3)    (PCs 4,5,6,
     30,99)                           Server)
Physical Connections
Device	Interface	Connected To	Interface	Cable Type
Router	Gi0/0/0	SW1	Gi0/1	Copper Cross-Over
SW1	Fa0/1	PC1	FastEthernet0	Copper Straight-Through
SW1	Fa0/2	PC2	FastEthernet0	Copper Straight-Through
SW1	Fa0/3	PC3	FastEthernet0	Copper Straight-Through
SW1	Fa0/24	SW2	Gi0/1	Copper Cross-Over
SW2	Fa0/1	PC4	FastEthernet0	Copper Straight-Through
SW2	Fa0/2	PC5	FastEthernet0	Copper Straight-Through
SW2	Fa0/3	PC6	FastEthernet0	Copper Straight-Through
SW2	Fa0/24	Server	FastEthernet0	Copper Straight-Through
VLAN Architecture
VLAN ID	Name	Subnet	Gateway	Purpose	Devices
10	SALES	192.168.10.0/24	192.168.10.1	Sales Department	PC1, PC4
20	ENGINEERING	192.168.20.0/24	192.168.20.1	Engineering Team	PC2, PC5
30	IT	192.168.30.0/24	192.168.30.1	IT Department	PC3, PC6
99	MANAGEMENT	192.168.99.0/24	192.168.99.1	Network Management	Server, Switches
?? Key Features Implemented
1. VLAN Segmentation
Department-based network isolation

Port-based VLAN assignment

Consistent across multiple switches

2. Trunk Configuration
802.1Q trunking between all devices

Native VLAN set to 99 (non-default for security)

Explicit allowed VLAN lists (10,20,30,99)

3. Inter-VLAN Routing
Router-on-a-Stick implementation

Subinterfaces for each VLAN with 802.1Q encapsulation

DHCP relay for automatic addressing

4. Network Services
DHCP server per VLAN with excluded addresses

DNS configuration (8.8.8.8)

Default gateway assignment per VLAN

?? Troubleshooting Encountered
Issue: Native VLAN Mismatch
Problem: CDP reported native VLAN mismatch between switches causing STP to block trunk port.

Error Message:

text
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (99), with Switch GigabitEthernet0/1 (1).
Root Cause: SW1 configured with native VLAN 99, SW2 using default VLAN 1.

Resolution: Configured matching native VLAN 99 on SW2 trunk port.

Proof of Fix:

text
%SPANTREE-2-UNBLOCK_CONSIST_PORT: Unblocking GigabitEthernet0/1 on VLAN0099. Port consistency restored.
Full documentation: troubleshooting-native-vlan-mismatch.md

? Verification Results
Connectivity Tests
? Intra-VLAN communication (PC1 to PC4 - same VLAN)

? Inter-VLAN communication (PC1 to PC2 - different VLANs)

? Server accessibility from all VLANs

? DHCP automatic addressing (all PCs receive IPs)

Protocol Verification
? CDP showing correct neighbor information

? STP ports in forwarding state

? Trunk links operational with matching native VLAN

? Routing table complete with all VLAN subnets

Command Verification Outputs
text
SW1# show vlan brief
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    
10   SALES                            active    Fa0/1
20   ENGINEERING                      active    Fa0/2
30   IT                               active    Fa0/3
99   MANAGEMENT                       active    Fa0/24
text
SW1# show interfaces trunk
Port        Mode             Encapsulation  Status        Native vlan
Fa0/24      on               802.1q         trunking      99

Port        Vlans allowed on trunk
Fa0/24      10,20,30,99
?? Configuration Files Summary
1. Switch 1 Configuration
Hostname: SW1

VLANs: 10, 20, 30, 99

Access Ports: Fa0/1 (VLAN10), Fa0/2 (VLAN20), Fa0/3 (VLAN30)

Trunk Port: Fa0/24 (to SW2) with native VLAN 99

Management: VLAN99 with IP 192.168.99.2/24

2. Switch 2 Configuration
Hostname: SW2

VLANs: 10, 20, 30, 99

Access Ports: Fa0/1 (VLAN10), Fa0/2 (VLAN20), Fa0/3 (VLAN30), Fa0/24 (VLAN99)

Trunk Port: Gi0/1 (to SW1) with native VLAN 99 (corrected from mismatch)

Management: VLAN99 with IP 192.168.99.3/24

3. Router Configuration
Hostname: R1

Subinterfaces: Gi0/0/0.10 (VLAN10), .20 (VLAN20), .30 (VLAN30), .99 (VLAN99)

DHCP Pools: VLAN10_POOL, VLAN20_POOL, VLAN30_POOL, VLAN99_POOL

IP Routing: Enabled

?? How to Use This Project
For Recruiters/Reviewers
Review the documentation/ folder for technical details

Check screenshots/ for visual proof of working implementation

View verification/ for test procedures and results

Examine config/ files for configuration expertise

Open .pkt file in Packet Tracer to explore live configuration

For Learning/Replication
Open packet-tracer-files/vlan-project-complete.pkt in Cisco Packet Tracer

Study configuration files in config/ directory

Follow test procedures in verification/test-procedures.txt

Modify and experiment with different scenarios

Try breaking things and troubleshooting (change native VLAN, remove trunk config, etc.)

?? Screenshot Evidence Included
Topology diagram with all connections

Configuration screenshots of all devices

Error messages and resolution steps

Verification command outputs (show vlan brief, show interfaces trunk)

Successful ping tests between all devices

?? Related Files
Complete Troubleshooting Report: troubleshooting-native-vlan-mismatch.md

Technical Specifications: technical-specifications.md

Verification Procedures: verification/test-procedures.txt

?? Contact & Links
Emmanuel Mukumbwa
CCNA Certified Network Engineer

