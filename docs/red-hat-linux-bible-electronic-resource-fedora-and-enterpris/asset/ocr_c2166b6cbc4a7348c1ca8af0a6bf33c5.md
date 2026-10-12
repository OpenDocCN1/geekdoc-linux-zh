+   * **Routers** — If you have a LAN or other type of network in your home or organization that you want to connect to the Internet, you can share an Internet connection. You do this by setting up a router. The router connects to both your network and the Internet, providing a route for data to pass between your network and the Internet.

+   * **Firewalls and IP masquerading** — To keep your private network somewhat secure, yet still allow some data to pass between it and the Internet, you can set up a firewall. The firewall restricts the kind of data packets or services that can pass through the boundary between the private and public networks. If your network uses private addresses, or if you just want to protect the addresses of computers behind your firewall, you can use techniques such as Network Address Translation (NAT) or IP masquerading.

> **NOTE**: Although you can set up a firewall to filter packets on any computer on your private network, firewalls are typically configured most stringently on the machine that routes packets between the public and private networks. In this way, intruders can be stopped before they get on your private network and security can be relaxed somewhat between your computers behind the firewall.

+   * **Proxies** — You can bypass some of the configuration required to allow the computers on your LAN to communicate directly with the Internet by configuring a proxy server. With a proxy server, a computer on your LAN can run Internet applications (such as a Web browser) and have them appear to the Internet as if they are actually running on the proxy server.

> **CROSS-REFERENCE**: You can read about firewalls in Chapter 14. IP masquerading and proxy servers are described in the "Enable forwarding and masquerading" and "Setting up Red Hat Linux as a Proxy Server" sections later in this chapter.

# Internet domains

You can’t read a magazine, watch a TV commercial, or open a cereal box these days without hitting a *something.com.* When a company, organization, or person wants you to connect to them on the Internet, it relies on the uniqueness of its particular domain name. However, within that domain name, the company or organization to which it has been assigned can arrange its content however it chooses.

Internet domains are organized in a structure called the *domain name system* (DNS). At the top of that structure is a set of *top-level domains* (or TLDs). Some of the top-level domains are used commonly in the United States, although they are available for worldwide use. TLDs such as edu (for colleges and universities), gov (for United States government), and mil (for United States military sites) were among the most used TLDs in the early Internet. In more recent years, com (for commercial sites) has experienced the most growth.

The us domain was added to include U.S. institutions, such as local governments and elementary schools, as well as to individuals within a geographical region of the United States.