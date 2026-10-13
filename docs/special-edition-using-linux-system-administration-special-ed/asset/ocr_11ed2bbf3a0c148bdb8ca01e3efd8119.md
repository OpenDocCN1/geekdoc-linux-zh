# TABLE 19.3 CONTINUED

| Number | Name | Required By |
|---|---|---|
| 8 | `echo-request` | ping |
| 11 | `time-exceeded` | traceroute |

> **Note**
> 
> The `!` (not) flag cannot be used for ICMP names.

> **Tip**
> 
> Do not block ICMP type 3 messages. They are used by TCP and UDP applications. ICMP packets are used to indicate failure for protocols such as TCP and UDP. If you block these packets you will never receive Host unreachable or No route to host errors; connections will just wait for a reply that never comes. While not fatal in most cases, the failure to receive these messages can be irritating and problematic when troubleshooting connectivity problems.
> 
> ICMP packets are also used in MTU discovery. The TCP implementations in Linux use MTU discovery to calculate the largest packet size that can be sent to a destination without fragmenting. Fragmenting slows performance, especially when occasional fragments are lost. MTU discovery works by sending packets with the Don't Fragment bit set, and then sending smaller packets if it gets an ICMP packet indicating Fragmentation Needed but DF Set (`fragmentation-needed`). This is a type of `destination-unreachable` packet, and if it is never received, the local host will not reduce MTU, and performance will be extremely poor or non-existent.

It is common to block all ICMP redirect messages (type 5) because these can be used to manipulate routing. However good IP stacks have safeguards against this type of manipulation, and therefore this is generally not considered a significant risk.

# SPECIFYING AN INTERFACE

The interface to match is specified with the `-i` option. An interface is the physical device on which a packet arrives or through which a packet leaves the firewall system. The input chain controls the interface for incoming packets. The output chain and the forward chain control the interface for outgoing packets.

You can specify an interface that currently does not exist, but is expected to be operational in the future. When the interface comes up, any existing rules will begin applying to that interface. This is very useful for dial-up PPP links where interfaces come into existence and then cease to exist with regularity.

An interface name that ends with a `+` will match all interfaces which begin with that string. For example, the `eth+` option will match all Ethernet interfaces.