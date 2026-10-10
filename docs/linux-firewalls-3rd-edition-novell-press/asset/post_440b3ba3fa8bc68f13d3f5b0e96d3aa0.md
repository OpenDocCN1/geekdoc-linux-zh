
# Don't Forget ARP

Address Resolution Protocol, or ARP, is the protocol used to link a physical device such as a network card to an IP address. Network devices use a 48-bit address (known as a MAC address) that is unique across all devices in a given segment. Although sometimes devices have the same MAC address, this is quite rare within the same network segment.

When capturing traffic in a network, you will encounter ARP packets at varying frequencies as devices locate one another as they pass traffic. ARP requests are broadcast so that all devices will see them. However, most ARP replies are unicast so that only the requesting device will see the reply. ARP traffic is not normally passed between network segments. Therefore, a router can be configured to provide proxy ARP service so that it can answer for ARP requests in multiple network segments.

# Hostnames and IP Addresses

People like to use words to name things, such as giving computers names like `mycomputer.mydomain.example.com`. Technically, it's not the computer that's being named, but the network interface on the computer. If the computer has multiple network cards, each card will typically have a different name and address, and will most likely be on a different network in a different subdomain.

Hostname elements are separated by dots. In the case of `mycomputer.mydomain.example.com`, the leftmost element, `mycomputer`, is the hostname. The `.mydomain`, `.example`, and `.com` are elements of the domains this network card is a member of. Network domains are hierarchical trees. What is a domain? It's a naming convention. The hierarchical domain tree represents the hierarchical nature of the global domain name service (DNS) database. DNS maps between the symbolic names people give to computers and networks and the numeric addresses the IP layer uses to uniquely identify network interfaces.

DNS maps in both directions: IP address to name and name to IP address. When you click on a URL in your web browser, the DNS database is consulted to find the unique IP address associated with that hostname. The IP address is passed to the IP layer to use as the destination address in the packet.

# IP Addresses and Ethernet Addresses

Whereas the IP layer identifies network hosts by their 32-bit IP address, the subnet or link layer identifies the Ethernet card by its unique 48-bit Ethernet address, or MAC address, which the manufacturer burns into the card. IP addresses are passed between the endpoint hosts to identify themselves. Ethernet addresses are passed between adjacent hosts and routers.

Ordinarily, the Ethernet address could be ignored in a firewall discussion. The Layer 2 hardware Ethernet address is not visible to the Layer 3 IP level or Layer 4 transport level. As you'll see in later chapters, iptables, the Linux firewall administration program, has the extended capability to access and filter on the MAC address. There are specialized uses for this firewall functionality, but it's important to remember that Ethernet addresses do not pass end-to-end across the network. Ethernet addresses are passed between adjacent network interfaces, or hosts and routers. They are not passed through a router unchanged.

# Routing: Getting a Packet from Here to There

Neither a residential site nor most businesses are likely to run routing protocols such as RIP or OSPF. In these cases, routing tables are set up statically, by hand. There's a hint in there. If you're running a routing protocol such as RIP, chances are that you don't need to be: you could operate a more efficient network without that unnecessary overhead. Typically, most sites have a default gateway device, which is the network that interface packets are sent on when the destination address's route is unknown. The service provider usually provides a single router address, which is the default Internet gateway for the site's local network.

# Service Ports: The Door to the Programs on Your System

Network-based services are programs running on a machine that other computers on the network can access. The service ports identify the programs and individual sessions or connections taking place. Service ports are the numeric names for the different network-based services. They are also used as numeric identifiers for the endpoints of a particular connection between two programs. Service port numbers range from 0 to **65535**.

Server programs (that is, *daemons*) listen for incoming connections on a service port assigned to them. By historical convention, major network services are assigned well-known, or famous, port numbers in the lower range from 1 to **1023**. These port number-to-service mappings are coordinated by the Internet Assigned Numbers Authority (IANA) as a set of universally agreed-on conventions or standards.

An advertised service is simply a service available over the Internet from its assigned port. If your machine isn't offering a particular service, and someone tries to connect to the port associated with that service, nothing will happen. Someone is knocking on the door, but no one lives there to answer. For example, HTTP is assigned to port 80 (though, again, there's no reason why you couldn't run it on port 8080, 20943, or any available port). If your machine isn't running an HTTP-based web server and someone tries to connect to port 80, the client program receives a connection shutdown message as an error message from your machine indicating that the service isn't offered.

The higher port numbers from 1024 to 65535 are called unprivileged ports. They serve a dual purpose. For the most part, these ports are dynamically assigned to the client end of a connection. The combination of client and server port number pairs, along with their respective IP host addresses, and the Transport protocol used, uniquely identifies the connection.

Additionally, ports in the 1024 through 49151 range are registered with the IANA. These ports can be used as part of the general unprivileged pool, but they are also associated with particular services such as SOCKS or X Window servers. Originally, the idea was that services offered on the higher ports were not running with root privilege. They were for use by user-level, nonprivileged programs. The convention may or may not hold in any individual case.

# Service Name-to-Port Number Mappings

Linux distributions are supplied with a list of common service port numbers. The list is found in the `/etc/services` file.

Each entry consists of a symbolic name for a service, the port number assigned to it, the protocol (TCP or UDP) the service runs over, and any optional nicknames for the service. Table 1.5 lists some common service name-to-port number mappings, taken from Red Hat Linux.

### Table 1.5
Common Service Name-to-Port Number Mappings

| PORT NAME | PORT NUMBER/PROTOCOL | ALIAS |
|---|---|---|
| ftp | 21/tcp | - |
| telnet | 23/tcp | - |
| smtp | 25/tcp | mail |
| nicname | 43/tcp | whois |
| domain | 53/tcp | nameserver |
| domain | 53/udp | nameserver |
| finger | 79/tcp | - |
| http | 80/tcp | www www-http |
| pop3 | 110/tcp | pop-3 |
| auth | 113/tcp | authentication tap ident |

| PORT NAME | PORT NUMBER/PROTOCOL | ALIAS |
|---|---|---|
| nntp | 119/tcp | readnews unread |
| ntp | 123/udp | - |
| https | 443/tcp | - |

Note that the symbolic names associated with the port numbers vary by Linux distribution and release. Names and aliases differ; port numbers do not.

Also note that port numbers are associated with a protocol. The IANA has attempted to assign the same service port number to both the TCP and the UDP protocols, regardless of whether a particular service uses both transport modes. Most services use one protocol or the other. The domain name service uses both.

# A Typical TCP Connection: Visiting a Remote Website

As an illustration, a common TCP connection is going to a website through your browser (connecting to a web server). This section illustrates the aspects of connection establishment and ongoing communication that will be relevant to IP packet filtering in later chapters.

What happens? As shown in Figure 1.6, a web server is running on a machine somewhere, waiting for a connection request on TCP service port **80**. You click on the link for a URL in Netscape. Part of the URL is parsed into a hostname; the hostname is translated into the web server’s IP address; and your browser is assigned an unprivileged port (for example, TCP port **14000**) for the connection. An HTTP message for the web server is constructed. It’s encapsulated in a TCP message, wrapped in an IP packet header, and sent out. For our purposes, the header contains the fields shown in Figure 1.6.

Additional information is included in the header that isn’t visible at the packet-filtering level. Nevertheless, describing the sequence numbers associated with the SYN and ACK flags helps clarify what’s happening during the three-way handshake. When the client program sends its first connection request message, the SYN flag is accompanied by a synchronization sequence number. The client is requesting a connection with the server and passes along a starting sequence number it will use as the starting point to number all the rest of the data bytes the client will send.

The packet is received at the server machine. It’s sent to service port **80**. The server is listening to port **80**, so it’s notified of an incoming connection request (the SYN connection synchronization request flag) from the source IP address and port socket pair (*your IP address, 14000*).
