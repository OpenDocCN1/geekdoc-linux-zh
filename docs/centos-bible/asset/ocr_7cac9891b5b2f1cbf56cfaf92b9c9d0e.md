```
# service iptables save
```

This copies all the current rules to the /etc/sysconfig/iptables file, from which the rules are read each time you reboot your system. If the new rules don't work, just copy the iptables.save file back to the original iptables file.

+   5. At this point, you may want to restart your network as follows:

```
# /etc/init.d/network restart
```

+   6. Then, to restart your firewall, type the following:

```
# /etc/init.d/iptables restart
```

+   7. To see if your new rules have gone into effect, type iptables -L. To view NAT rules, type iptables -L -t nat

If the route to the Internet from Linux is being provided by a dial-up connection, you probably want to turn on on-demand dialing (as described earlier in this chapter).

# Configuring Network Clients

In this example, there are a variety of Linux and Windows operating system clients on a LAN. One Linux computer has a connection to the Internet and is set up to act as a router between the Internet and the other computers on the LAN (as described previously). To be able to reach computers on the Internet, each client must be able to do the following:

+   Resolve the names it requests (e.g. www.centos.org) into IP addresses.

+   Find a route from the local system to the remote system, using its network interfaces.

Each Linux client computer knows how to find another computer's address based on the contents of the /etc/hosts.conf, /etc/hosts, and /etc/resolv.conf files. The contents of the host.conf file, by default, are the following:

```
order hosts,bind
```

This tells your system to check for any hostnames (hosts) that you request by first checking the contents of the /etc/hosts file and then checking with name servers that are identified in the /etc/resolv.conf file. In our case, we will put the addresses of the few hosts we know about on our private network (whether on the LAN, direct connection, or other network interface) in the /etc/hosts file. Then, the system knows to resolve addresses using a DNS server (bind) based on addresses of name servers we add to the /etc/resolv.conf file.

Next, each client machine must know how to get to the Internet. Do this by adding a default route, sometimes called a gateway, to each client. To permanently add a default route on the client Linux system, do the following:

+   1. Set the default route to point to the router. This entails setting the GATEWAY or GATEWAY-DEV value in the /etc/sysconfig/network file as described in the previous procedure. This time, the address will point to the LAN interface of the router.