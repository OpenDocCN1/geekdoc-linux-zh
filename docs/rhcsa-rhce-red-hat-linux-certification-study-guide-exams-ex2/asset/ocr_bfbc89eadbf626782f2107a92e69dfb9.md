# Make Sure the Firewall Is Running

Once desired changes are saved to the /etc/sysconfig/iptables configuration file, it's important to make sure the Firewall is in operation, with the new rules. Since the reload option is not available in the /etc/init.d/iptables script, you'll need to do so with the following command:

> exam Watch
> *It's critical to understand how to secure a Red Hat Enterprise Linux system against unauthorized access.*

```
# service iptables restart
```

As discussed in Chapter 11, this is functionally equivalent to the /etc/init.d/iptables restart command.

# IP Masquerading

Red Hat Enterprise Linux supports a variation of NAT called IP masquerading. IP masquerading supports Internet access from multiple computers with a single public IP address. IP masquerading maps multiple internal IP addresses to that single valid external IP address. That helps as all public IPv4 address have now been allocated. While IPv4 addresses are often still available from these third parties, at a price. That cost is one more reason for IP Masquerading. On the other hand, systems on IPv6 networks may not need masquerading, as it's relatively easy for many requesting users to get their own subnet of public IPv6 addresses. Nevertheless, even on IPv6 networks, masquerading can help keep that system secure.

> exam Watch
> *The RHCE objectives specify the use of iptables to configure network address translation.*

IP Masquerading is a fairly straightforward process. It's implemented on a gateway or router, where the system has two or more network cards. One network card is connected to an outside network such as the Internet, and the second (and additional) network card is connected to a LAN. The card connected to the outside network may connect through an external device such as a cable "modem" or Digital Subscriber Line (DSL) adapter.

The following assumptions are made for the configuration:

+   - The public IP address is assigned to the network card that is directly connected to the outside network.