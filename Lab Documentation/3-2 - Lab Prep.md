For this week's lab - you need to use your completed Packet Tracer file from Week 2 lab or use this starter file Download this starter file.

1. We will be adding a server directly to the East-Core-Switch on the Mgmt VLAN (vlan 1)

2. Using the "End Devices" objects, drag a Generic Server (3rd from left) to the left of the East Core Switch

3. Give your server an IP address from your Mgmt VLAN subnet (I recommend 10.x.y.2) and set the Gateway to 10.x.y.1

use "x.y." based on your VLAN Subnet table for the MGMT subnet
4. Configure East-Core-Switch Fast Ethernet port 0/3 as an access port on VLAN 1

5. Assign an ip address from your Mgmt VLAN Subnet to East Core Switch (use 10.x.y.1) . Refer to your Tech Journal or Lab 2-1 for the proper commands.

Important NOTE: The MGMT VLAN is Vlan 1 - the default vlan on the switch.
The VLAN 1 interface is disabled (shutdown) by default.  From the VLAN 1 interface config in the CLI, you must issue the following command after you enter the IP address and mask:
no shutdown
6. Connect your server (F0) to East Core on F0/3.

7. You should be able to ping from your server to the router and other IP's on the network.

8. Submit screenshot of successful ping