Remember how annoying it was to assign the IP addresses to all of the clients in Packet Tracer in the last lab...

In this lab, you will configure a DHCP Server in Packet Tracer to assign IP's to laptops and workstations.

Using your Packet Tracer file from the Lab Prep, do the following:

I. Find and review your Subnet Table from Last Week's Lab

II. Configure the DHCP Server

Rename the generic server you enabled in the Lab Prep to DHCP-01
Go to the Services tab and enable DHCP
Change the Start Address of serverPool to 100 in the last octet
serverPool is the Default Pool and cannot be removed. 
You will use this pool for VLAN 1 Management
Create a Pool for each of your FacStaff, Student, Lab1, and Lab2 VLANs
Default gateway is the router address for that VLAN (e.g. FacStaff, Student...)
Leave DNS at 0.0.0.0
Start IP address -the first IP that you want to assign (I suggest starting at 20,50, or 100)
Subnet Mask for that VLAN- get this correct!
Maximum Users - set this close to the requirements in your Subnet Table
TFTP leave at 0.0.0.0
III. Test your DHCP Server

Add a workstation directly to East-Core-Switch on VLAN1 (use FA0/4 or other open interface)
Workstation should be able to get an IP address from the DHCP server (look at IP Configuration) -you can also try ipconfig /renew from the command line
IV. Configure DHCP Relay

East-Core-Switch is the router for your VLANs. Remember - DHCP requests are broadcasts and cannot cross a router without help!
To get DHCP broadcasts from your user VLANs (100, 110, 130, 140), you need to tell the router to forward them to your DHCP server.
This is done with the "ip helper-address" vlan interface configuration
On East-Core-Switch, go into the interface configuration for FacStaff VLAN 100 (config t, interface vlan 100)
Use "ip helper-address" to provide the IP address of the DHCP server
Repeat steps for each user vlan
V. Configure Clients to use DHCP

Go into the configuration on your Admin, Student, and Lab Workstations, Laptops and change the Gateway from static to DHCP
Your devices should get DHCP addresses
All of your systems should be able to ping each other.
When complete - submit your Packet Tracer file

Tech Journal:

You will need to set up DHCP in future labs so it is important to record the steps in your Tech Journal

Create an entry for "DHCP in Packet Tracer" and include the steps and commands you need to set it up such as:

How to create pools
Working with serverPool
Assigning ip helper addresses
Any issues you encountered
Tech Journal does not need to be submitted this week but will be checked and graded in the future so please update!