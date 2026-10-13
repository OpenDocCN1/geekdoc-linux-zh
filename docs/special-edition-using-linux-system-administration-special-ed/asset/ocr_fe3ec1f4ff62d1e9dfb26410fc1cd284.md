# Proxy Server Firewalls

Proxy servers are used primarily to monitor and control outbound traffic. For example, you can run the squid proxy server to cache Web and FTP data for all users in your network. This can lower the Internet bandwidth requirement and speed up access by supplying the cached data. Proxies also provide detailed logs of all data transfers. Because proxy servers can examine the payload of packets, they can also be used to filter inappropriate content.

There are two types of proxy servers:

+   - **Applications proxy servers**—These provide separate proxy services for each protocol that needs to be run through the proxy server. A typical example of an application proxy server is the squid proxy server that provides HTTP and FTP application proxy servers. Squid is available at `http://www.squid-cache.org/`.
+   - **SOCKS proxy servers**—These provide generalized proxy services for applications which know how to communicate with a SOCKS proxy server. Information about SOCKS proxy servers is available at `http://www.socks.nec.com/`.

# IP Masquerading Proxy Servers

Linux uses IP masquerading to provide the functionality of one-to-many NAT (Network Address Translation). NAT provides two major benefits as a firewall tool:

+   - Using addresses that are not routed over the Internet for a private network makes the internal network into a black box that cannot be directly examined from the Internet. The topology of the internal network is hidden from external networks, which enhances the security of the internal network significantly.
+   - The need for a large number of registered valid IP addresses for each host on your network is eliminated and only a small number of valid addresses is required.

IP masquerading allows all internal machines to hide behind the firewall machine and use its IP address to access the Internet. To all machines on the Internet the traffic from the internal hosts appears to originate from the single masquerading firewall machine. This provides a foundation for a very secure internal network. The Internet only sees the well-secured firewall machine and nothing beyond that. Breaking through a properly secured Linux IP masquerading host into the internal network is an extremely difficult task generally considered virtually impossible.

> **Note:** The key here is that your IP masquerading firewall must be properly configured and secured. If it is incorrectly configured and secured, your internal network can easily be as accessible as if you had no firewall at all.