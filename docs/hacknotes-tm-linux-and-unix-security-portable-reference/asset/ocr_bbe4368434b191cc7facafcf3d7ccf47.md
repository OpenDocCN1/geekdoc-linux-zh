the route. If the TTL of an IP packet equals 0, then the particular gateway will send an “ICMP Time to Live Exceeded” packet back to the source. Thus, the traceroute tool determines the IP addresses of the gateways along the way to the destination by looking at the source of the “ICMP Time to Live Exceeded” packets returned.

The traceroute tool sends UDP packets by default, but it can be made to use ICMP packets when run with the -I switch.

![](bbox=[0.09, 0.3, 0.14, 0.35])

> Some gateways and firewalls are configured to either drop incoming UDP and ICMP packets and/or drop outgoing “ICMP Time to Live Exceeded” packets. This will cause traceroute to skip over such gateways and firewalls.

Sometimes, firewalls are configured to allow packets whose source port is 20 (FTP-Data) or 53 (DNS). The -p option in traceroute can therefore be used to set the source port of outgoing UDP packets in order to attempt to take advantage of such firewall rules.

![](bbox=[0.07, 0.47, 0.12, 0.52])

# ### Prevent Incoming Traceroute Requests

The following steps can be taken in order to prevent incoming traceroute requests from succeeding:

+   * Configure your firewall to drop incoming UDP and ICMP packets.
+   * Configure your firewall to drop outgoing “ICMP Time to Live Exceeded” packets.
+   * If you must allow incoming UDP packets for DNS, configure your firewall to allow only incoming UDP packets with source port 53 (DNS) originating from specific DNS server IP addresses.

# ## SUMMARY

This chapter showed you how potential intruders might use publicly available information to gain sensitive and critical information about the target organizations including how to obtain administrative contacts, domain names, network blocks, hostnames, and MX records of the target’s network. After obtaining any of this information, an intruder will have a better idea of the target organization’s network architecture and administrative weaknesses. The information you gained from the techniques described in this chapter is instrumental in your learning about the process of network scanning and identification, which is the next step of the hacking methodology.