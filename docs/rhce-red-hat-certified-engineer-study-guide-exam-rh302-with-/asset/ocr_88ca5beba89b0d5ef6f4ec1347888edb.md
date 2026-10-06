Another way to enable IP forwarding is to manipulate the /proc file system. Issue the command
echo "1" >/proc/sys/net/ipv4/ip_forward
drawback of this method is that you will have to reissue the command
each time you reboot the system.

# Routing Configuration

To configure routing requires the route command, which is contained in the net-tools package automatically installed during the standard installation procedure. You can use the route command directly; but many Red Hat Linux system administrators prefer to configure routing using linuxconf, which invokes route based on information you supply using dialog boxes.
Concept, the routing configuration consists of a table that contains routing rules. Each rule has two components:

+   - A destination IP address, which can refer to a host, subnetwork, or network.
- An interface, which refers to a network adapter.
- An optional gateway IP address, which refers to a host that routes packets to the specified destination. If the gateway IP address is omitted, the destination IP address is assumed to be directly reachable via the specified interface.

> PPP and SLIP devices always act as gateways. You don't need to—and
should't—specify a gateway address for a destination reachable via PPP or SLIP.

# Using linuxconf to Specify Routing Rules

To specify routing rules for accessing a network using linuxconf, select Config ➤ Networking ➤ Client Tasks ➤ Routing and Gateways ➤ Other Routes to Networks from the linuxconf menu. The Route to Other Networks, shown in Figure 29.3, will appear. Specify the destination IP address and (optionally) the network mask of the network. Also specify the IP address of the gateway host on the local network that provides access to the network.