The network address for such a network would be the first three segments of the IP address, 192.168.0. The network netmask would cover those first three segments, using the number 255.255.255.0. This mask is used to determine the host and network parts of an IP address. The broadcast address, 192.168.0.255 in this example, is used to allow an administrator to contact all hosts at once. You would then use these three IP addresses when configuring a host.

In the sample network used in these examples, there are three hosts, each with its own IP addresses and hostnames listed here. The network address, netmask, and broadcast address are the same as those just described:

```
192.168.0.1
192.168.0.2
192.168.0.3
```

Note See Chapters 34 and 38 for detailed information on IP addresses and DNS server set up.

The firewall should run only on the gateway. Furthermore, the gateway will have two network connections, one for the local network and an Internet connection device for the Internet. Make sure that the firewall is applied to the device used as the Internet device, not to your local network. On redhat-config-securitylevel, you do this by making the local network device a trusted device. In the network example used here, the firewall is run on the eth0 network device (the first Ethernet card), which functions as the gateway. The local network is connected through the eth1 network device (the second Ethernet card).

# Assigning IP Addresses: static and dynamic

You can assign IP addresses either statically or dynamically. Static addresses are entered manually into each machine, whereas dynamic addresses are assigned automatically by a single DHCP server running on one of the machines. If your network is very small, like two or three machines in a home network, then it may make sense to use static addressing. In this case, you manually assign each IP address by physically logging into each computer as the root user and running redhat-config-network to assign an IP address to