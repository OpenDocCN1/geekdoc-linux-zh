# Firewalls

A firewall is a computer that stands between a trusted network (such as your internal network) and an untrusted network (such as the Internet), and controls what traffic passes between them. It is an essential piece of the information security puzzle.

There are two general types of firewalls (which may be combined): application-level firewalls (known as proxies), and packet-filtering firewalls. A packet-filtering firewall simply allows or disallows packets depending on their content. Most packet-filtering firewalls determine what packets to allow or disallow based on the source or destination addresses, source or destination port, and whether the packet is part of an ongoing conversation.

An application-level firewall or proxy acts as an intermediary between client and server programs. Instead of connecting directly to the server, a client application connects to the proxy and asks it for the information. The proxy opens a connection to the server, sends the request, and continues to pass information back and forth between server and client (see Figure 7.9).

# Figure 7.9
Packet-filtering and application-level firewalls are compared.

![](bbox=[0.2985, 0.4915, 0.7925, 0.6665])

Both types of firewalls have advantages and disadvantages, and many sites implement both. A packet-filtering firewall is regarded as less secure than a proxy-based firewall, since a proxy-based firewall will actually make a network connection on your behalf, and pass back all of the data it receives. In other words, when a proxy-based firewall is well set up, the only way to access systems outside your network is to use your firewall as a proxy to retrieve data for you. The design of proxy-based firewalls can thus completely shield your internal network from outside influences.