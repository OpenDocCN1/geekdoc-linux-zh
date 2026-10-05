# Chapter 21 Network Management and Debugging

# 21.15 EXERCISES

E21.1 You are troubleshooting a network problem, and netstat -rn gives you the following output. What is the problem and what command would you use to fix it?

| Destination | Gateway | Genmask | Flags | MSS | Window | irtt | Iface |
|---|---|---|---|---|---|---|--|
| 128.138.202.0 | 0.0.0.0 | 255.255.255.0 | U | | 40 | 0 | eth0 |
| 127.0.0.1 | 0.0.0.0 | 255.255.255.0 | U | | 40 | 0 | lo |

+   * E21.2 Write a script that monitors a set of machines and notifies an administrator by email if a machine becomes unresponsive to ping for some amount of time. Don't hard-code the list of machines, the notification email address, or the amount of time to determine unresponsive behavior.

+   * E21.3 Experiment with changing the netmask on a machine on your local network. Does it work? Can you reach everything at your site? Can other machines reach you (e.g., ARP requests or DHCP discover packets)? Explain your findings. (Requires root access).

+   * E21.4 Use the traceroute command to discover routing paths on your network.
a) How many hops does it take to leave your facility?
b) Are there any routers between machines on which you have accounts?
c) Can you find any bottlenecks?
d) Is your site multihomeded?

+   * E21.5 Design a MIB that includes all the variables as a Linux sysadmin might want to query or set. Leave ways for the MIB to be extended to include important new sysadmin variable for you.

+   * E21.6 Use wireshark or shark to capture traffic that illustrates the following protocols. For TCP connections, include and indicate the initial and final packets. Submit clean, well-formatted output. (Requires root).
a) ARP
b) ICMP echo request and reply
c) SMTP
d) HTTP
e) DNS
f) Samba
g) SSH

+   * E21.7 Set up Cacti graphs to show the packets transmitted to and from a local router. This project requires an SNMP package to query the router, and you must know the router's read-only community string.