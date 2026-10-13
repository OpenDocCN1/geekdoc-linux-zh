# CERTIFICATION OBJECTIVE 10.02

# Firewalls and Network Address Translation

Typically, firewalls reside between internal LANs and outside insecure networks such as the Internet. A firewall can be configured to examine every network packet that passes into or out of your LAN. When configured with appropriate rules, it can filter out those packets that may pose a security risk to the systems on the LAN.

However, to follow the spirit of the recommendations from the NSA, you'll configure a firewall on every system. While Network Address Translation uses the same iptables command, its use is generally still most appropriate for those systems on the gateway or router between a LAN and an outside network.

# Definitions

Firewalls based on the iptables command work by reading the headers of each packet of network data. Based on the information contained in the headers, iptables-based rules can be used to filter each packet. To understand how packet filtering works, you have to understand a little bit about how information is sent across networks.

Before a message is sent over a network, that message is broken down into smaller units called packets. Administrative information, including the type of data, the source address, and the destination address, is added to the header of each packet. The packets are reassembled when they reach the destination computer. A firewall examines the fields in each header. Based on existing rules, the firewall may then take one of four actions with that packet:

+   - Allow the packet into the system.
+   - Forward the packet to other systems if the current system is a gateway or router between networks.
+   - Reject the packet with a message sent to the originating IP address.
+   - Drop the packet without sending any sort of message.

Whatever the result, the decision can be logged. If there are a substantial number of packets that are rejected or dropped, a log file may be useful.

RHEL 6 comes with everything you need to configure a system to be a firewall, including the iptables and ip6tables commands for IPv4 and IPv6 networks.