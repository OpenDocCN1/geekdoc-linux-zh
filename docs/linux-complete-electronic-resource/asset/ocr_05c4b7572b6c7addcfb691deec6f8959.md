It is perfectly legal to specify an interface that currently does not exist; the rule will not match anything until the interface comes up. This is extremely useful for dial-up PPP links (usually interface ppp0) and the like.

As a special case, an interface name ending with a + will match all interfaces (whether they currently exist or not) that begin with that string. For example, to specify a rule which matches all PPP interfaces, the -i ppp+ option would be used.

The interface name can be preceded by a ! to match a packet that does not match the specified interface(s).

# Specifying TCP SYN Packets Only

It is sometimes useful to allow TCP connections in one direction but not the other. For example, you might want to allow connections to an external WWW server, but not connections from that server.

The naive approach would be to block TCP packets coming from the server. Unfortunately, TCP connections require packets going in both directions to work at all.

The solution is to block only the packets used to request a connection. These packets are called SYN packets (OK, technically they're packets with the SYN flag set and the FIN and ACK flags cleared, but we call them SYN packets). By disallowing only these packets, we can stop attempted connections in their tracks.

The -y flag is used for this; it is only valid for rules which specify TCP as their protocol. For example, to specify TCP connection attempts from 192.168.1.1: -p TCP -s 192.168.1.1 -y

Once again, this flag can be inverted by preceding it with a !, which means every packet other than the connection initiation.

# Handling Fragments

Sometimes a packet is too large to fit down a wire all at once. When this happens, the packet is divided into fragments and sent as multiple packets. The other end assembles the fragments to reconstruct the whole packet.

The problem with fragments is that some of the specifications listed above (in particular source port, destinations port, ICMP type, ICMP code, or TCP SYN flag) require the kernel to peek at the start of the packet, which is only contained in the first fragment.