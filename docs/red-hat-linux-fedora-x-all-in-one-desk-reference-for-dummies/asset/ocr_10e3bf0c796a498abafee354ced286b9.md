# 570 Setting Up Simple Firewalls

These rules ensure that the internal network communicates only with the bastion host (or hosts).

Like the dual-homed host, the bastion host also runs an application gateway that provides proxy services for various Internet services, such as TELNET, FTP, SMTP, and HTTP.

# Application gateway

The bastion host or the dual-homed host is the system that acts as the intermediary between the Internet and the protected internal network. As such, that system serves as the internal network's gateway to the Internet. Toward this end, the system runs software to forward and filter TCP/IP packets for various services, such as TELNET, FTP, and HTTP. The software for forwarding and filtering TCP/IP packets for specific applications are known as proxy servers. Figure 3-4 illustrates a proxy server's role in a firewall.

A proxy server accepts a connection for a specific protocol, such as FTP, and forwards the request to another server. In other, the proxy server acts as a proxy for an actual server. Because it acts as a gateway for a specific application (such as HTTP or FTP), a proxy server is also known as an application gateway.

Figure 3-4: A proxy server lets internal hosts access Internet servers.

![](bbox=[0.253, 0.536, 0.848, 0.843])