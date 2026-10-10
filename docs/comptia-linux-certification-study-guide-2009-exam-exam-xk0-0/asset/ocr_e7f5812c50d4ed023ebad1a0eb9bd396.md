+   8. A user wants to ensure that his wireless card installed correctly in his system only connects to his company's network. This network has an SSID of mycorp and uses WPA2 for added security. How would you ensure this occurs?
+   A. iwconfig essid mycorp
+   B. iwconfig default mycorp
+   C. iwconfig default_ssid mycorp
+   D. iwconfig noroam essid mycorp

+   9. You have just started work as an IT contractor in a company called mycorp. You have been given a laptop with a static address as you manage some of the routers, and these have access control lists (ACLs) on them allowing your IP to access them. You want to check that your name-server, which is currently set on your machine to be 10.10.100.67, is correct. What command would most likely give you the correct result?
+   A. traceroute 10.10.100.67
+   B. nslookup 10.10.100.67
+   C. dig dns.mycorp.com
+   D. nslookup dns.mycorp.com

+   10. You are working in a medium-sized company and have added a new server to the network. A static IP address of 10.10.100.45 has been assigned to it. The routing table is shown below:

| Destination | Gateway | Netmask | Flags | Metric | Ref | Use | Iface |
| :---------- | :------ | :------ | :---- | :----- | :-- | :-: | :---- |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | 0 | 0 | lo |
| 10.10.100.45 | * | 255.255.255.0 | U | 0 | 0 | 0 | eth0 |

What command will add a default route to 10.10.100.1?

+   A. /sbin/route add default 10.10.100.1
+   B. /sbin/default route add 10.10.100.1
+   C. /sbin/route add default gw 10.10.100.1
+   D. /bin/route add default gw 10.10.100.1

+   11. You wish to set up the default editor in your environment to be the vim editor instead of the current setting of vi. Which would be the best solution to achieve this?

+   A. Modify the /etc/env.conf file to set the default editor environment variable EDIT to be vim
+   B. Modify the /etc/env.conf file to set the default editor environment variable EDITOR to be vim