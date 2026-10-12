# **Listing 7-4** *The /etc/sysconfig/network file*

```
```
NETWORKING=yes
FORWARD_IPV4=yes
HOSTNAME=gateway.nitec.com
DOMAINNAME=nitec.com
```
```

The most important setting here is `FORWARD_IPV4=yes`, which enables IP forwarding in the kernel.

> **Tip**
> 
> You must have IP forwarding support built into the kernel. You can use the `cat /proc/sys/net/ipv4/ip_forward` command to see whether IP forwarding is enabled in a running kernel. If the output is 1, then IP forwarding is set; a value of 0 signifies that IP forwarding is turned off. You can also turn it on or off by inserting a value of 1 or 0 using the `echo n > /proc/sys/net/ipv4/ip_forward` command, where *n* is either 1 or 0.

Listings 7-5 and 7-6 show the two interface (`eth0` and `eth1`) files.

# **Listing 7-5** *The /etc/sysconfig/network-scripts/ifcfg-eth0 file*

```
```
DEVICE=eth0
IPADDR=192.168.1.126
NETMASK=255.255.255.128
NETWORK=192.168.1.0
BROADCAST=192.168.1.127
ONBOOT=yes
```
```

# **Listing 7-6** *The /etc/sysconfig/network-scripts/ifcfg-eth1 file*

```
```
DEVICE=eth1
IPADDR=192.168.1.254
NETMASK=255.255.255.128
NETWORK=192.168.1.128
BROADCAST=192.168.1.255
ONBOOT=yes
```
```