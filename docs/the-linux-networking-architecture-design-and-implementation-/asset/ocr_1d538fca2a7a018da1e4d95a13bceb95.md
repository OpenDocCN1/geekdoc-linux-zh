# C.5 Using tcpdump for Network Analysis

-x causes each packet (except the LLC header) to be output in hexadecimal format. The number of output bytes can be defined by the option -s (default = 68). You can use an expression to output only packets of the LAN that meet this expression.

**Expressions** Expressions consist of one or several primitives. A primitive, in turn, is built from a qualification parameter and a value (name or number).

There are three types of qualification parameters:

+   * Types define the type to be qualified. Three types are available: host, net, and port; host is the default if no type is specified.
* The direction defines the transmit direction of the packet to be analyzed. The direction can be either src, dst, src or dst and src dst. src stands for incoming packets and dst for transmitted packets. src or dst is assumed if nothing is specified.
* The protocol specifies that only packets of a specific protocol type should be analyzed. Any of the protocols that can be specified are ether, fddi, ip, arp, rarp, tcp, and udp.

If several protocols should be analyzed, then the types can be OR-linked. If no special protocol is specified, then all protocols matching the specified type are analyzed.

# **Examples**

+   * src tux: All packets from computer tux.
* (src tux) and (ip or arp): All packets from tux, but only IP or ARP packets.
* port 80: All packets of the TCP or UDP protocols where the port is equal to 80.

Notice that keywords and arithmetic expressions can be used in addition to this syntax. Complex conditions are achieved by AND, OR, and NOT linking (e.g., host tux AND NOT port 80 AND NOT port 21).

# **Other Conditions**

+   * less length: Only packets with the maximum of the specified length are considered.
* greater length: Only packets with at least the specified length are considered.
* broadcast: The packet must be a broadcast message.
* multicast: The packet must be a multicast message.

# **Arithmetic Conditions**

Expression Relop expression: The expression is an arithmetic integer expression and may include one of the following three operators:

Binary operators (as in the programming language C: + - */ & |).