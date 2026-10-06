# Part IV: Fedora RHEL Network and Server Setup

The Internet and the other computers on the LAN (as described previously). To be able to reach computers on the Internet, each client must be able to do the following:

+   - Resolve the names it requests (for example, www.redhat.com) into IP addresses.
- Find a route from the local system to the remote system, using its network interfaces.

Each Linux kernel knows how to find another computer's address by the contents of the /etc/host.conf, /etc/hosts and /etc/resolv.conf files. The contents of the host.conf file, by default, is the following:

```
order hosts,bind
```

This tells your system to check for any hostnames (hosts) that you request by first checking the contents of the /etc/hosts file and then checking with name servers that are identified in the /etc/resolv.conf file. In our private network, we will put the addresses of the hosts we know about in our network (whether on the LAN, direct connection, or other network interface) in the /etc/hosts file. Then, the system knows to resolve addresses using a DNS server (bind) based on addresses of name servers we added to the /etc/resolv.conf file.

Next, each client machine must know how to get to the Internet. By adding a default route (some call it gateway) to each client. To permanently add a default route on the client system, do the

+   1. Set the default route to the router. This entails the GATEWAY or GATEWAYDEV value in the /etc/config/network file as described in the previous procedure. (This time, the address will point to the LAN interface of the router.)
2. Restart your network interfaces by typing the following as root user:
3. When the computer comes back up, type the following:

```
# /etc/init.d/network restart

# netstat -r
Kernel IP routing table
```

| Destination | Gateway | Genmask | Flags | MSS Window | irtt Iface |
|---|---|---|---|---|---|-|
| 10.0.0.0 | * | 255.255.255 | U | 0 | 0 | eth0 |
| 169.254.0.0 | 0.0.0.0 | 255.255.255 | U | 0 | 0 | eth0 |
| default | 10.0.0.1 | 0.0.0.0 | UG | 0 | 0 | eth0 |

You can see that the default gateway was set to the IP address 10.0.0.1 on the eth0 Ethernet interface. Assuming that router is ready to route all your packets to the Internet, your Linux kernel is now ready to use to find all IP addresses that you request that you not already know where to find. (The netstat -r command provides the same output as the /sbin/route command.)