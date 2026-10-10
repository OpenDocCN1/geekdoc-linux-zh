# Backgrond Material

We've seen the lo and eth interfaces. The tr interfaces are for token-ring networks, sl is for SLIP interfaces (an older protocol for running IP over a serial link), and ppp are the A Point-to-Point protocol interfaces (discussed in Chapter 13).

# Interface Configuration

Each interface has a configuration script called /etc/sysconfig/network-scripts/ifcfg-ifname. For example, interface eth0 has a configuration script /etc/sysconfig/network-scripts/ifcfg-eth0. This script looks something like this:

```
#!/bin/sh

>>>Device type: ethernet
>>>Variable declarations:
DEVICE=eth0
IPADDR=192.168.2.3
NETMASK=255.255.255.0
NETWORK=192.168.2.0
BROADCAST=192.168.2.255
GATEWAY=192.168.2.1
ONBOOT=yes
DYNAMIC=...
>>>End variable declarations
REMIP=0.0.0.0
MTU=1500
```

The variables have the following meanings:

+   - DEVICE is the interface name.
+   - IPADDR is the IP address of the interface.
+   - NETMASK is the network mask of the interface.
+   - NETWORK is the network address of the interface.
+   - BROADCAST is the broadcast address of the interface.
+   - GATEWAY is the IP address of a gateway machine. If the network has no gateway, this variable is set to none. The presence of a gateway causes the network scripts to set up a default route using the gateway.
+   - ONBOOT is either yes or no. If it is yes, the interface upstarts when the computer is booted. This is appropriate for Ethernet interfaces, but might not be appropriate for modem lines.