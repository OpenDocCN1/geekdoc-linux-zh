+   • A network host must be configured with the IP address of a DNS server to resolve domain names into IP addresses.  
+   • A network host must be configured with the IP address of the segment’s default gateway router for it to communicate with hosts on other network segments.  
+   • IPv6 addresses are composed of eight four-character hexadecimal numbers, separated by colons instead of periods.  
+   • Public networks use globally unique, registered IP addresses.  
+   • Private networks use nonroutable, unregistered, nonunique IP addresses.  
+   • Within each class of IP address are blocks of addresses called private or reserved IP addresses.  
+       • 10.0.0.0–10.255.255.255 (Class A)  
+       • 172.16.0.0–172.31.255.255 (Class B)  
+       • 192.168.0.0–192.168.255.255 (Class C)  
+   • You can use a NAT router to hide a private network behind one or more public interfaces.  
+   • To install an Ethernet interface in a Linux system, you first need to install the network board in the system and connect it to the network medium.  
+   • Next, you need to load the appropriate kernel modules for the board.  
+   • The network board should have an alias created for it named eth0.  
+   • Additional boards will have aliases of eth1, eth2, and so on assigned.  
+   • You can enter ifconfig at the shell prompt to view the details of your installed network interfaces.  
+   • To assign an IP address to a network interface, enter ifconfig interface IP_address netmask subnet_mask broadcast broadcast_address at the shell prompt.  
+   • To make IP address assignments persistent, enter them in the appropriate file within the /etc/sysconfig/network directory.  
+   • Enter your organization’s DNS server address in the /etc/resolv.conf file.  
+   • Enter your segment’s default gateway router address in the /etc/sysconfig/network/routes file.  
+   • Enter ifdown at the shell prompt to bring a network interface down.  
+   • Enter ifup to bring a network interface back up.  
+   • To dynamically assign an IP address to a Linux host, enter dhclient interface at the shell prompt.  
+   • Linux includes a variety of command-line utilities you can use to test and monitor the network.  
+   • Use ping to test connectivity between systems. The syntax is ping destination_host.  
+   • Use the netstat command to view a variety of network interface information using the -a, -l, -s, and -r options.