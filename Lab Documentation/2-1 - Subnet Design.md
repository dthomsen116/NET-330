Class lab to Design Network for a School and Build in Packet Tracer.

For this lab, your assigned network is:

10.x.0.0/16 where x is the number of the day you were born.

1. Design Addressing

Complete the following table

VLAN	VLAN_NAME	Hosts Needed	Network	Netmask	Router Address
1	Management	250			
100	FacStaff	200			
110	Student	450			
130	StuLab1	35			
140	StuLab2	35			
200	StuWireless	900			
210	FSWireless	650			
Get approval from instructor before moving on

 

Start Building Network in Packet Tracer

 Once your address design is approved, start configuring the network as started in the following Packet Tracer File

NET-330-Module2-Subnet_starter-file-19.pktDownload NET-330-Module2-Subnet_starter-file-19.pkt

1. Edge Configuration - use the following guidelines:

Configure Edge Switches

Add vlans to the vlan database
100 and 110 to all
130 (Lab1) in East-02 switch only
140 (Lab2) in West-02 switch only
All edge switches assigned VLAN 100 (FacStaff) on ports 4-12 
All edge switches assigned VLAN 110 (Student) on ports 13-20
East-Edge-02 assigned VLAN 130 (Lab1) on ports 21-24
West-Edge-02 assigned VLAN 140 (Lab2) on ports 21-24
Useful Commands:

(config)interface range FastEthernet 0/x-y (let's you configure multiple ports at one time)
(config-if-range)switchport access vlan x (defines the vlan for all ports in the range)
Configure End User Devices

Assign FacStaff PC's IP's from VLAN 100 (make sure netmask and gateway are correct)
Assign Student PC's IP's from VLAN 110
Assign Lab PC's appropriate IP's
Connect Devices to Edge Switch

Connect devices with Copper to appropriate ports
Verification that Step 1 is complete:

Ping devices on same vlan and same switch
Not able to ping different vlans or different switch
2. Configure Trunking

Configure trunk ports for Core switches

Add vlans 100, 110, 130, and 140 to the vlan database on Core Switches
Configure FastEthernet 0/1 and 0/2 as trunk ports for the appropriate vlans
Configure trunk ports for Edge switches

Configure FastEthernet 0/1 as trunk port for the appropriate vlans
3. Connect Edge Switches to Core

 Create Cross-over cable connection between edge switch and core switch trunk ports
Verification: You should now be able to ping between two systems on the same VLAN on different switches

4. Enable Routing

The Core Switches are multi-layer and can route
We will use the EAST-Core Switch as the Router
Enable routing on the the East-Core Switch
Assign the router addresses from the table in step 1 to:
VLANs 100,110,130, 140 to East-Core
Useful Commands:

(config)ip routing (turns on routing on multilayer switches)
(config)interface vlan 100 (brings you into vlan interface config mode)
(config-if)ip address 10.25.100.1 255.255.255.0 (set the ip address of 10.25.100.1 for vlan 100 on a routing switch)
NOTE: This only needs to be set on the router-switch acting as the gateway for the vlan
Verification: You should now be able to ping between two systems on different VLANs in EAST 

5.  Configure East-West Trunk

Configure Gigabit Ethernet 0/1 on both East and West core switches as trunk ports for defined vlans
Copper "cross-over" connector to connect those trunk ports
Verification: You should be able to ping between all devices!

LAB Submission: Working Packet Tracer File

 

---------------------------------------------------------

Tech Journal Entry for Lab 2-1 Subnet Design

Commands to navigate different modes on a Cisco Switch/Router (enable, config t...) and how you know what mode you are in
Commands to create VLANS on switch
Setting access and trunk ports on switch
Configure interfaces in "ranges"