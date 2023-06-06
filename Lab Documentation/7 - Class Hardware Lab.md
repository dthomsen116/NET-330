Goal: Have PC's on both of your group's internal VLANs access the public web server

Subnet/VLAN Assignments

Vlan Name	VLAN ID	Group	Network Address	Subnet Mask	Default GW
Backbone	1	All	153.104.1.0	/24	153.104.1.1 (Border)
G1-Admin	100	1	172.16.10.0	/24	172.16.10.1
G1-Staff	110	1	172.16.11.0	/24	172.16.11.1
G2-Admin	200	2	172.16.20.0	/24	172.16.20.1
G2-Staff	210	2	172.16.21.0	/24	172.16.21.1
G3-Admin	300	3	172.16.30.0	/24	172.16.30.1
G3-Staff	310	3	172.16.31.0	/24	172.16.31.1
G4-Admin	400	4	172.16.40.0	/24	172.16.40.1
G4-Staff	410	4	172.16.41.0	/24	172.16.41.1
G5-Admin	500	5	172.16.50.0	/24	172.16.50.1
G5-Staff	510	5	172.16.51.0	/24	172.16.51.1
Public	N/A	Border/None	153.104.5.0	/24	153.104.5.1 (GW) 153.104.5.10 (WWW)
Backbone IP Assignments

Border Router	153.104.1.1
G1 MLS	153.104.1.10
G2 MLS	153.104.1.20
G3 MLS	153.104.1.30
G4 MLS	153.104.1.40
G5 MLS	153.104.1.50
Network Diagram

Screen Shot 2022-10-12 at 10.58.06 AM.png

 

Goals:

Configure edge switch with appropriate VLANs
Use bootable kali thumbdrives for PCs
Configure MLS as Distribution Router and to act as Default GW for your local vlans
Configure NAT on MLS so that all internal addresses use the PUBLIC backbone address for that distribution area (PAT)
Configure MLS with a default route to send traffic to 153.104.1.1 (border router)
Internal PCs should be able to access the public web server (153.104.5.10)
Submit:

Screenshot of MLS config
Screenshot of successful access of 153.104.5.10 webpage from Admin PC
Screenshot of successful access of 153.104.5.10 webpage from Staff PC
One submission per group is fine - but make sure to put everyones name on it!