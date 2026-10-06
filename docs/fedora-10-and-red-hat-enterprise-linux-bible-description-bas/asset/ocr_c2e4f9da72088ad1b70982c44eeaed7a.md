# Chapter 16: Connecting to the Internet 687

Internet, you use a fully qualified domain name to identify a host computer. For example, in the domain handsonhistory.com, a host named baskets would have a fully qualified domain name of baskets.handsonhistory.com.

Within an organization, you should choose a host-naming scheme that makes sense to you. For example, for handsonhistory.com, you could have hostnames to different crafts (baskets, decoys, weaving, and so on). Some organizations use the names from Norse mythology such as thor, oddin, and loki, or beer brands such as summit, namesake, and so on.

> TIP: For some naming schemes, see http://c2.com/cgi/wiki?NamesGivenToComputers.

+   - Routers If you have a LAN or other type of network in your home or organization that you want to connect to the Internet, you can share an Internet connection. You do this by setting up a router. The router connects to your network and the Internet, providing a route to pass data between your network and the Internet. This is especially useful if you want to connect to the Internet over a dial-up or broadband connection, since your Linux box can act as a router and you can share the connection among all your computers.

+   - Firewalls and IP masquerading To keep your private network secure, yet still allow data to pass between it and the Internet, you can set up a firewall. The firewall restricts the kind of data packets or services that can pass through the boundary between private and public networks. If your network uses private addresses, or if you just want to protect the addresses of computers behind your firewall, you can use techniques such as Network Address Translation (NAT) or IP masquerading.

> NOTE: Although you can set up a firewall to filter packets on any computer on your private network, firewalls are typically configured most strongly on the machine that routes packets between the public and private networks. In this way, intruders can be stopped before they get on your private network and security can be relaxed between your computers behind the firewall.

+   - Proxies You can bypass some of the configuration required to allow the computers on your LAN to communicate directly with the Internet by configuring a proxy server. A proxy server can store (referred to as caching) Internet objects (such as data from Web and FTP servers) so clients of that server don't have to contact the server originating data each time it is requested. With a proxy server, a computer on your LAN can also run Internet applications (such as a Web browser) and have them appear to the Internet as if they are actually running on the proxy server.

> CROSS-REFERENCE: You can read about firewalls in Chapter 14, IP masquerading servers are described in the sections "Enable forwarding and masquerading" and "Setting Up Linux as a Proxy Server" later in this chapter.