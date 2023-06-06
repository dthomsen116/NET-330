NAT Configuration - PAT (Port Address Translation):

In Dynamic Nat, translations are made IP to IP. So you need as many global IP address as you have inside local address. That's an issue if you have few global IP address and hundreds of inside local address to translate. In such situations, you need to use PAT.

For this lab,  we are going to configure the topology below so that the private address PC's (on the 192.168.0.0/24 network) will all use 30.0.0.120 as their (shared) Public IP address

 

Lab Topology

 

Use NAT-PAT-Lab-2.pkt Download NAT-PAT-Lab-2.pktas starter file.

In this example our internal network is using the 192.168.0.0 network and we have one public ip addresses to use- 30.0.0.120.

Router1  is going to be the NAT device

NAT3.PNG

 

Configure Router Interfaces

On Router 1: FE 0/0 192.168.0.1/24 and Serial 0/0/0 30.0.0.1/8

On Router 2: FE 0/0 20.0.0.1/8 and Serial 0/0/0 30.0.0.2/8

Configure Routing

On Router 1: Set the Default Route (or Gateway of Last Resort) to Router 2

ip route 0.0.0.0 0.0.0.0 30.0.0.2
At this point, there should be no connectivity between the PC's and the external networks/server. Ping will fail to 20.0.0.2

Configure PAT on Router 1

1. Define "Inside" and "Outside" interfaces

2. Create Address Pool named "test" for the Public IP addresses that 192.168 clients can use. It only has 1 IP in the pool (30.0.0.120)

R1(config)#ip nat pool test 30.0.0.120 30.0.0.120 netmask 255.0.0.0
3. Create an access-list that defines which internal IP's can use the Public IP pool test

R1(config)#access-list 1 permit 192.168.0.0 0.0.0.255
4. Assign pool and access rule to interface with nat statement - basically saying that access-list 1 (192.168 addresses) can be translated to the PAT IP' from pool "test" when going from the "inside" to "outside". Overload states that the IP can be used by many (up to 64,000) clients.

R1(config)#ip nat inside source list 1 pool test overload


 If PAT is working, you should be able to connect the web service on the server (20.0.0.2) from the browser on multiple PC's

To verify PAT, go to R1 and use this sh ip nat translations command.  It show how TCP ports are used to track connections in the  NAT Table :

R1#show ip nat translations
Pro  Inside global     Inside local       Outside local      Outside global
icmp 30.0.0.120:1        192.168.0.7:1      20.0.0.2:1         20.0.0.2:1
icmp 30.0.0.120:2        192.168.0.7:2      20.0.0.2:2         20.0.0.2:2
icmp 30.0.0.120:3        192.168.0.7:3      20.0.0.2:3         20.0.0.2:3
icmp 30.0.0.120:4        192.168.0.7:4      20.0.0.2:4         20.0.0.2:4
 

Submit Screenshot of IP NAT Table

Tech Journal Entries for Lab 6-2 NAT PAT

Commands to configure PAT with explanation so you can do it in future!