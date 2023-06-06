For this lab - you will design and build a small enterprise network (in Packet Tracer) for a community healthcare facility.

Pre-Lab: 

Open Packet Tracer and go to - Options - Preferences - Miscellaneous
Set Auto File Backup Interval to 1 minute
Save your workspace as NET-330-Lab-4-1-name
You need to save the file before auto backup starts working
Take Notes throughout on any issues you run into and how you fix them.  Needed for Tech Journal

I. Design

1. Plan you IP Address/Subnet scheme:

You will use 10.X.0.0/8 where X is your workstation number
Create a table for your IP subnets that includes
Network Address, Subnet Mask, VLAN ID, Host Ranges, Default Gateway (Router) and DHCP pool ranges
You need to include the following subnets:
Default Subnet (VLAN 1) used for networking services such as DHCP and DNS (150 IP's)
"Clinic" VLAN used for Dr.'s and Nurses (300 IP's)
"Visitor" VLAN used by patients and guests (300 IP's)
"Office" VLAN used for administrative staff (300 IP's)
"Counseling" VLAN used by mental health practice (150 IPs)
Review with instructor before moving on to Step 2
SUBMIT: Subnet Table
2. Design the network in Packet Tracer:

Create Border/Distribution, Core, and Edge boundaries
NOTE: we will be using 1 Distribution area in this lab for simplicity - and the single Distribution Switch/Router is also the Border Router
Edge: North Wing switch, South Wing switch, and Counseling Center switch (South Wing):
use 2960's
Core: North-Core, South-Core, and Data-Center-Core switches
use 2960's
Add 2 servers to the core - one will be for DNS and one for DHCP
Border/Distribution: Hospital Router (Use 3560 Multilayer Switch)
Review with instructor before proceeding
SUBMIT: Screenshot of Packet Tracer Workspace
This is an example of a Single Distribution Area Design using a school scenario.  Your design for this lab should be similar:



For reference - this would be an example of using Multiple Distribution Areas - if we were doing a larger design or campus - it would fully use the Internetworking Hierarchical Model:



 

II. Build

1. Configure Hospital Router

Enable Routing
Add VLANs to Router
Add IP addresses to VLAN interfaces
Configure trunk ports to connect to core switches
2. Configure North-Core Switch (can copy to South Later)

 Add VLANS
Configure trunk ports to connect router and edge switch
3. Configure North Wing Edge Switch (can copy to South later)

Assign 6 ports to Clinic
Assign 4 ports to Visitor
Assign 6 ports to Office
Configure trunk port to connect core switch
4. Configure Data-Center-Core switch

Only uses VLAN 1 (so minimal config required)
Connect Data-Center-Core to Router (Trunk not required on either side)
5. Configure DHCP Server

Assign DHCP server proper address
Create DHCP pools for the client VLANs
Remember to turn DHCP Service "On" in the PT services window
Connect server to Data Center Core switch
To get DHCP working - don't forget "Helper"
SUBMISSION: Screenshot of a PC with proper DHCP address (config page in PT)
SUBMISSION Screenshot of PC's on different subnets pinging one another
6. Configure clients in North Wing Edge

You should now have DHCP working so it should be easy
Make sure connecting to the correct ports for the VLAN
SCREENSHOT: North PC pinging South PC
7. Configure DNS

Assign appropriate IP address to the DNS server
Connect to Data-Center-Core
Enable DNS services
Create A Records for your two servers:
ns.station-number-word.com (e.g. ns.twelve.com)
dhcp.station-number-word.com (e.g. dhcp.twelve.com)
Update DHCP server to assign DNS server to clients
Verify that clients can resolve server IP's
SUBMIT: Screenshot of successful DNS resolution
8. Bonus Activities:

Finish South Wing
Configuring Counseling Center Edge Switch and clients
Add additional servers to data center (web...) and configure DNS records
Submit screenshots of any additional configuration
 