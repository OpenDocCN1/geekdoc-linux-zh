# ## Summary

+   - DHCP lets you configure automatically the three fundamental networking parameters on machines on your network. This is necessary for diskless machines and very convenient for other machines. It greatly simplifies network management
+   - by allocating and re-using addresses from a pool, DHCP can share a small number of addresses among a large set of machines that are not all in use at the same time
+   - the DHCP client and server converse using UDP broadcast packets. The full conversation consists of four packets: DISCOVER, OFFER, REQUEST, ACKNOWLEDGE
+   - the server allocates an IP address to a client for a fixed lease time. Near the expiry time, a client can ask the server to renew its lease. Even when a client shuts down, the server will normally not allocate this address to another client unless it runs out of available addresses. This enables clients to keep the same IP address over very long periods
+   - DHCP broadcast packets can't pass through routers. To allow DHCP to work on routed networks, DHCP relay agents pass DHCP broadcasts to the full DHCP elsewhere on the network, and in turn broadcast the replies they receive, allowing the DHCP client to hear the reply.

# ## What's next?

The next chapter looks at many other commonly used protocols and how they work.

# ## Notes and further reading

The almost-original DHCP RFC is very readable and understandable, giving background on why DHCP is necessary, its design criteria, and how it works:

+   - RFC-1541 **October 1993** *Dynamic Host Configuration Protocol*

This has now been superseded by:

+   - RFC-2131 **March 1997** *Dynamic Host Configuration Protocol*

For notes on using DHCP with Linux, with the **dhcpcd** client:

+   - <http://www.linuxdoc.org/HOWTO/mini/DHCP/index.html>

The current DHCP standard can server only class-ful routes, i.e. the netmask for the route is derived from the class A, B, or C type of the address specified. As this isn't adequate nowadays when almost everyone uses classless (CIDR) addressing, an amendment to the DHCP standard has been proposed to include classless route as a DHCP option.

A dated (1999) but very good FAQ:

+   - <http://www.dhcp-handbook.com/dhcp_faq.html> *DHCP FAQ*