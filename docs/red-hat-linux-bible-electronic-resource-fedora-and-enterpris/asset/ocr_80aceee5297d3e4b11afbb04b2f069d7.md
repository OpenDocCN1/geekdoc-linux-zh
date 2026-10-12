+   • Packets on the LAN that are not addressed to a known computer on the LAN are forwarded to the router (that is, the Red Hat Linux system acting as a router). So, each client identifies that Red Hat Linux system as the gateway system.
+   
+   • The Red Hat Linux "router" firewall is set up to receive packets from the local LAN, then forwards those packets to its other interface (possibly a PPP connection to the Internet). If the LAN uses private IP addresses, the firewall is also configured to use IP masquerading or Network Address Translation.

The following sections describe how to set up the Red Hat Linux router, as well as the client computers from your LAN (Red Hat Linux and MS Windows clients) that will use this router. Using Red Hat Linux as a router also provides an excellent opportunity to improve the security of your Internet connection by setting up a firewall to filter traffic and hide the identity of the computers on your LAN (IP masquerading).

# Configuring the Red Hat Linux router

To configure your Red Hat Linux computer as a router, you need to have a few things in place. Here's what you need to do before you set up routing:

+   • **Connect to your LAN.** Add a network card and optionally set up the addresses in `/etc/hosts` to the computers on your LAN (as described in Chapter 15) or using DHCP (as described in Chapter 23).
+   
+   • **Connect to the Internet.** Set up a dial-up or other type of connection from your Red Hat Linux computer to your ISP. This is described earlier in this chapter in the section on setting up outgoing PPP connections.
+   
+   • **Configure your Red Hat Linux computer as a router.** See the rest of this section.

The type of IP addresses you are using on your LAN will have an impact on a couple of steps in this procedure. Here are the differences:

+   • **Private IP addresses** — If the computers on your LAN use private IP addresses (described in Chapter 15), you need to set up Linux as a firewall to do IP masquerading or NAT (as described in Chapter 14). Because those numbers are private, they must be hidden from the Internet when the Red Hat Linux router forwards their requests. Packets forwarded with masquerading or NAT look to the outside world as though they came from the Red Hat Linux computer forwarding the packets.
+   
+   • **Valid IP addresses** — If your LAN uses addresses that were officially assigned by your ISP or other registration authority, you don’t need to do IP masquerading or NAT.

# Enable forwarding and masquerading

With your Red Hat Linux computer’s LAN and Internet interfaces in place, follow the procedure below to set up Red Hat Linux as a router. Once this procedure is completed, any