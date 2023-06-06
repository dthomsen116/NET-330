Class Activity 1 - Configuring Static NAT

Configuring of static NAT is straight forward. In this example, we have a web server connected to Router 1. Our web server is using the Private IP address of 10.0.0.2.

Our goal is to "masquerade" the source IP so we want to use  a static "mapping" of 50.0.0.1 as the public IP address for this server.

Our task is to configure NAT on Router 1 to translate  to the web server's local IP of 10.0.0.2  to a public address of  50.0.0.1.

Network Diagram: We want 10.0.0.2 to be accessible as 50.0.0.1 from 30.0.0.2 

 static_nat_blank.jpgUs

Use the NAT-Static-Lab1.pkt Download NAT-Static-Lab1.pktFile as a starting point.

Configuration of Router Interfaces:

Configure interfaces on Router 1 (R1):

Router>enable
Router#configure terminal
Router(config)#hostname R1
R1(config)#interface fastethernet 0/0
R1(config-if)#ip address 10.0.0.1 255.0.0.0
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#interface serial 0/0/0
R1(config-if)#ip address 20.0.0.2 255.0.0.0
R1(config-if)#no shutdown
R1(config-if)#exit

 Configure Interfaces on Router 0 (R0)

Router>enable
Router#configure terminal
Router(config)#hostname R0
R0(config)#interface fastethernet 0/0
R0(config-if)#ip address 30.0.0.1 255.0.0.0
R0(config-if)#no shutdown
R0(config-if)#exit
R0(config)#interface serial 0/0/0
R0(config-if)#ip address 20.0.0.1 255.0.0.0
R0(config-if)#clock rate 64000
R0(config-if)#bandwidth 64
R0(config-if)#no shutdown
R0(config-if)#exit

 Configure Routing:

On Router 1:

R1(config)#ip route 30.0.0.0 255.0.0.0 20.0.0.1
On Router 0:

R0(config)#ip route 50.0.0.0 255.0.0.0 20.0.0.2


From the PC's, test connectivity by pinging the router address of 20.0.0.1 and 30.0.0.1

 As you have seen in the configuration, there is no direct route to 10.0.0.2 from the  30.0.0.0/8 network. So the PCs cannot reach it - test with ping and it should fail.

Configure Static NAT on Router 1

1. Define "Inside" and "Outside" on your NAT interfaces:

R1(config)#interface fastEthernet 0/0
R1(config-if)#ip nat inside
R1(config-if)#exit
R1(config)#interface serial 0/0/0
R1(config-if)#ip nat outside
R1(config-if)#exit
2. Create the Static Rule:

R1(config)#ip nat inside source static 10.0.0.2 50.0.0.1
You should now be able to ping the web server using it's NAT address of 50.0.0.1

Open up the web page of 50.0.0.1 on one of the PC's

Submit Screenshot of the PC successfully viewing the page at 50.0.0.1

TECH Journal Entries for Lab 6-1 Static NAT

Setting NAT interfaces
commands for static NAT with example