Server Load Balancing with HAProxy

For this lab, we will be using the open-source software HAProxy for web-server load-balancing. HAProxy is open-source and used by many of the most popular sites on the Internet.

I. Lab Set-Up

For this lab, you will need an HAProxy VM (link below) and 2 CentOS simple web servers (link below)

HAProxy VM Download

HAProxy: https://drive.google.com/file/d/0B0CNjprTQ-jAbEhqTERBZ3hiYUE/view?usp=sharing&resourcekey=0-do2Maqm2hRfVCIe4CBBGCQLinks to an external site.

CentOS Web Server VM Download

CentOS-Apache-Base: https://drive.google.com/file/d/0B0CNjprTQ-jAd1dlRVgycGVqMGs/view?usp=sharing&resourcekey=0-FUpbaqwPx2_IGMAT3yDfpQLinks to an external site.

Screen Shot 2022-04-15 at 9.12.34 AM.png

A. Configure 2 Web Servers in VMWare

Download the CentOS-Apache-Base-VM    (user: root, password: test3)   
Make a copy of the download - as you will need 2 CentOS-Apache-Base-VM's running
Start up a VM called "Server 1" using Bridged or NAT networking
Start up another VM (using the copy of the base VM) called "Server 2" using Bridged or NAT networking
Run dhclient to get an IP address on each
Make sure that the 2 servers can ping each other before proceeding
On each server, create a simple text file  /var/www/html/index.html with content that indicates the server-name/number
Start httpd (systemctl start httpd) on both servers
From your workstation browser, verify that you can reach the website on both server IP addresses before proceeding
B. HAProxy Server 

Download the HAProxy VM 
Launch VM using Bridged or NAT networking
Password: test3
Run dhclient to get an IP
Verify that you can ping the 2 web servers from the HAProxy server before proceeding
II. Configuring Load Balancing in HAProxy

A. Define the "Frontend"

In HAProxy - the "frontend: refers to the IP address that remote users will use to connect to the "balanced" servers.

On other vendor's Load Balancers, this is often referred to as the VIP (Virtual IP) as it is the IP address assigned to the pool of systems and not the physical servers themselves.  

In our lab - the IP address of the HAProxy server will be the VIP as it is handling the connections on behalf of the "backend servers"

edit /etc/haproxy/haproxy.cfg
Under "#define frontend" we will need to enter the following:
frontend web-srv-pool-1  (this creates a VIP for a server pool call web-srv-pool-1
bind *:80   (this says that the pool will use the HAProxy server's IP address and port 80)
default_backend web_servers  (the backend servers group is called "web_servers")
B. Define the Backend

Under the "# define backend" section in haproxy.cfg, enter the following
backend web_servers (creates a backend group called "web_servers")
balance roundrobin  (use the roundrobin method for load balancing)
server server1 ip_of_server1:80
server server2 ip_of_server2:80
Save your haproxy.cfg file
restart haproxy service
Use systemctl status haproxy to make sure haproxy is "active"
C. Testing HAProxy

From your workstation - browse to the HAProxy IP address
You should see either the Server1 or Server2 web page
Refresh - use different browsers etc. and you should see it switch between Server1 and Server2!
D. Submit screenshots of the Server 1 and Server 2 pages displayed in a browser with the HAProxy IP address

 

III. Enable HAProxy Logging

Logging is important for Load Balancing monitoring and troubleshooting.  We will configue rsyslog to log HAProxy info to /var/log/haproxy.log

A. Configure rsyslog config file /etc/rsyslog.conf  

 
HAProxy-Syslog.png
Make sure to do the last part - and restart rsyslog
B. Restart HAproxy

C. do a "tail -f /var/log/haproxy.log" and make connections from your workstation browser to your "frontend".  The connections should be logged

D. Submit screenshot of haproxy log showing roundrobin connection attempts

 IV. Configure Health Checks

Monitoring services on the backend servers to see if they are still responding can be an important component of server load balancers.  If a service is unresponsive, it is useful if the load balancer does not send any packets to that system.

HAProxy monitors systems through Health Checks.  By default, the HAProxy server tests the service on each backend server ever 2 seconds (configurable).  These tests can be simple TCP connections or more detailed checks to see if a certain protocol (e.g. HTTP) is responding or if a particular resource is returned (e.g. words on a web page).

A. Enable Health Checks for the Backend Servers

Edit the haproxy.cfg file
In the "backend" section add "check" after the server definitions
e.g. 
server             www01 10.0.0.31:80 check
Save the file and restart haproxy
B. Test Health Check for Down Servers

Run a tail -f /var/log/haproxy.log
shutdown Server2
Wait for a bit and monitor the log
You should see a "server2 is Down" message
Try and connect to the Frontend IP - you should only get Server1 responses
Restart Server2 (don't forget dhclient and to restart httpd)
You should see "server 2 is Up" message
C. Test Health Check for Down Services

Repeat the steps above (B.) but instead of shutting down Server 2 - just stop httpd
D. Submit screenshots of the haproxy.log showing server 2 going down and up again

V. Additional HAProxy Configurations

Many backend servers do not use standard ports so change the web server Apache listening ports on server1 and server2 from 80 to 8008
Hint: httpd.conf 
Update HAproxy for the changed ports
Frontend connection should still be port 80
Update the firewall on the web server(s) to allow port 8008 (firewall-cmd command)
Submit: screenshots of:
server listening on port 8008 (can browse directly to server using http://ip_of_server:8008Links to an external site.)
HAProxy balancing correctly (browsed to Frontend IP)
Update the HTTP Checks to look for specific URL
Edit haproxy.cfg
Under the "backend web_servers" configuration - add a httpchk option to perform a HEAD request for /index.html
HEAD requests will pull down the headers for that URL (not the whole file) so if index.html is not there, it will fail
Apache supports Virtual Hosts, so you will also need the "Host:" header
Syntax of option httpcheck
option httpchk METHOD URL Protocol\r\nHost:any_domain_name
METHOD is HTTP Method (HEAD,GET,PUT...)
\r\n is for a new line
example: option httpchk HEAD /status/check.html HTTP/1.1\r\nHost:slb-lab.com
you only need to add this line once.  It defines an option for any server that is being "check"-ed
For example, a backend server section might look something like:
server      www01      10.0.0.31:80                     check

server     www02       10.0.0.42:80                    check

option httpchk HEAD /status/check.html HTTP/1.1\r\nHost:slb-lab.com

Remember - the url has to be a page that exists on your server (/index.html in this lab)
When you have the correct line, Restart HAProxy
tail -f /var/log/haproxy.log
rename /var/www/html/index.html on server 1 or server 2
You should see a Layer 7 Down message in HAProxy
change back to index.html and HAProxy should mark server as UP
Submit: Screenshot of logfile showing Layer 7 Down/Up messages

