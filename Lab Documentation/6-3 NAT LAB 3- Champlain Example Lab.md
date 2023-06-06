Goals:

Configure IP addressing/gateways on all PC's and Servers using the IP Subnet Table provided
Configure PAT on CC Border Router so that Foster and Skiff PC's can ping the BT server.(45 POINTS)
Remember: Foster and Skiff are using private IP addresses (192.168....) - so they can use a shared public IP to access Internet services (such as the Burlington Telecom Server)
Must demonstrate that NAT is working by showing ip nat translation table.  You will need to ping the server from CC pc's to generate entries in the table
Hint: access lists can have more than one network in them - just enter a "access-list 1 permit..." line for each network that is allowed (Skiff and Foster)
Remember: make sure to use an IP from the Champlain Public Network as the PAT pool address
Use Lab 6-2 as a reference for the configuration
Configure Static NAT on Border Router so that BT Server can access the Ireland Pub Web Server(15 POINTS)
You want Internet users to be able to access your internal Public web server - but it is using a private address
Pub Web Server is assigned a 192.168.7.0/24 address - but needs to be reached on a 219.93.144.0 address by BT server
Use Lab 6-1 as a reference