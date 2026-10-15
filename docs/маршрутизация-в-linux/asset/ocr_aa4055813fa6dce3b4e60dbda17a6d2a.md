![](bbox=[0.48, 0.04, 0.66, 0.24])

# 9

# Inside the Commands

LINUX PROVIDES AN ARRAY OF NETWORKING commands to support network troubleshooting, IP configuration, and routing tasks. This chapter covers ifconfig, route, ping, traceroute, arp, netstat, and tcpdump. With the exception of tcpdump, these commands will likely be installed with a standard install of most Linux distributions. These commands (again with the exception of tcpdump) have their roots in earlier versions of BSD and AT&T's System V commands.

# ifconfig

ifconfig is the command used to bring interfaces into service and specify Layers 1 through 3 attributes, such as media type, speed, and network addresses. (Layer 1 covers the physical aspects of the network, such as twisted pair or coaxial cabling, and Layer 2 covers the data layer, including the media dependent network, such as Ethernet frames and media access control in Ethernet networks.) ifconfig is normally located in the /sbin/ directory, but the program can be run by nonroot users. However, only configuration changes can be carried out by root. With most versions of Linux, the ifconfig command is provided by the net-tools distribution, which is available at http://www.tazenda.demon.co.uk/phil/net-tools/.