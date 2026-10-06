# 366 Linux Administration: A Beginner's Guide

To enable support for the new nftables in your kernel, you will need the following to be enabled during kernel configuration: Network Packet Filtering, nf_tables, nf_tables conrack, IPv4_tables, and IPv6 nf_tables. Network Packet Filtering can be found under the → Networking Support → Networking Options → Network Packet Filtering (Netfilter).

Core nftables support can be found under the → Networking Support → Networking Options → Network Packet Filtering (Netfilter) → Core Netfilter Configuration → Netfilter_tables support.

nf_tables conrack can be enabled via → Networking Support → Networking Options → Network Packet Filtering Framework (Netfilter) → Core Netfilter Configuration

IPv4_tables is under Networking Support → Networking Options → Network Packet Filtering Framework (Netfilter) → IP: Net Configuration → IPv4_tables Support.

Finally, IPv6_tables support can be enabled via → Networking Support → Networking Options → Network Packet Filtering Framework (Netfilter) → IPv6: Net Configuration → IPv6_tables Support.

# Optional but Sensible Kernel Options

With the options just compiled into the kernel, you technically have to make Netfilter work for most applications. However, a few options can make life easier, provide additional security, and support some common protocols. For all practical purposes, you should consider these options as requirements. All of the following can be compiled as modules so only those in use are loaded into memory:

+   **FTP Protocol Support** This option is available once Connection Tracking is selected. With it, you can correctly handle FTP connections through NAT. Active FTP requires a separate connection from the server to be made to the client when transferring data (such as directory lists, file transfers, and so on). By default, NAT will not know what to do with server-initiated connection. With the FTP module, NAT will be given the intelligence to handle the protocol correctly and make sure that the associated connection makes it back to the appropriate client.

+   **IRC Protocol Support** This option is available once Connection Tracking is selected. If you expect users behind NAT will want to use Internet Relay Chat (IRC) to communicate with others on the Internet, this module will be required to correctly handle connectivity, IDENT requests, and file transfers.

+   **Connection State Match** This option is available once IP Tables support is enabled. With it, connection tracking gains the masterful functionality that was discussed in the “Connection Tracking and NAT” earlier in the chapter. To reiterate, it allows the matching of packets based on their relationship to previous packets. This should be considered a requirement for anyone configuring a system as a firewall.