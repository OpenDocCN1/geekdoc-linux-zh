# Proxy Server Implementation

A proxy server, also known as an application gateway, is a much more secure and flexible firewall solution than a pure packet filter. The proxy software can be configured to intercept network traffic. The proxy recognizes the request and sends the request to the server. In this way, the internal client never connects directly to the external server; thus, the proxy functions as the intermediary, communicating to both the client and the server. The major advantage is that the proxy software can permit or deny traffic based on the actual data in the packet, and not simply the header.

![](bbox=[0.26, 0.24, 0.93, 0.44])

# The iptables Program

Definition:

The *iptables* program is a firewall program in Linux that provides protection to the internal network. The iptables program uses rule sets, called *chains*, to implement *IP filtering*. There are three iptables: *filter*, *nat*, and *mangle*.

Example:

![](bbox=[0.25, 0.61, 0.93, 0.87])

Syntax

The syntax of the *iptables* program is `iptables [-t table] {commands} {chain/rule specification} [options/parameters]`.