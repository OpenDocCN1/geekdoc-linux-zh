For optimal security, use a dedicated system as a router. Because data transmission over a connection to the Internet—even over a broadband connection—is relatively slow, using a slower, older system as a router does not generally slow down a LAN. This setup also offers some defense against intrusion from the Internet. A workstation on the LAN can function as a router as well, but this setup means that you maintain data on a system that is directly connected to the Internet. The following sections discuss the security of each setup.

The examples in this section assume that the device named **eth0** connects to the Internet on 10.255.255.255 and that **eth1** connects to the LAN on 192.168.0.1. Substitute the devices and IP addresses that the local systems use. If you use a modem to connect to the Internet, you need to substitute **ppp0** (or another device) for **eth0** in the examples.

For the examples in this section to work, you must turn on IP forwarding. First give the following command and make sure everything is working:

```
$ sudo sysctl -w net.ipv4.ip_forward=1
net.ipv4.ip_forward = 1
```

If you want to forward IPv6 packets, give this command instead:

```
$ sudo sysctl -w net.ipv6.conf.all.forwarding=inet.ipv6.conf.all.forwarding = 1
```

Once you know that **iptables** is working correctly, follow the instructions in `/etc/sysctl.conf` and uncomment one or both of the following assignments to make the kernel always perform IP forwarding for IPv4 and/or IPv6:

```
# Uncomment the next line to enable packet forwarding for IPv4
#net.ipv4.ip_forward=1

# Uncomment the next line to enable packet forwarding for IPv6
#net.ipv6.conf.all.forwarding=1
```

After making this change, give the command `/sbin/sysctl -p` to apply the change and to make sure that there are no typographical errors in the configuration file.

# ## Connecting Several Clients to a Single Internet Connection

Configuring the kernel of the router system to allow clients on multiple local systems on the LAN to connect to the Internet requires you to set up IP masquerading, or SNAT (source NAT). IP masquerading translates the source and destination addresses in the headers of network packets that originate on local systems and the packets that remote servers send in response to those packets. These packets are part of connections that originate on a local system. The example in this section does nothing to packets that are part of connections that originate on the remote