# What Is a Firewall?

+   Linksys (www.linksys.com/) makes a number of small office/home office router products that use SPI technologies. These are very inexpensive and easy to configure.

+   Cisco (www.cisco.com) is a very well-known and highly respected vendor for many different types of network products, including router firewalls that use SPI technology.

> FYI: Stateless Packet Filtering

Stateful packet inspection is clearly the preferred method. The natural follow-up question is: What about stateless packet filtering? This term is not generally used by security professionals; it merely denotes the standard packet filtering method.

# Application Gateway

An application gateway (also known as application proxy or application-level proxy) is a program that runs on a firewall. This type of firewall derives its name from the fact that it works by negotiating with various types of applications to allow their traffic to pass the firewall. In networking terminology, negotiation is a term used to refer to the process of authentication and verification. In other words, rather than looking at the protocol and port the packet is using, an application gateway will examine the application and the server-side application to which it is trying to connect. It will then determine if particular client traffic is permitted through the firewall. This is significantly different from a packet filtering firewall, which examines the packets and has no knowledge of what sort of application sent them. Application gateways enable the administrator to allow access only to certain specified types of applications, such as web browsers or FTP clients.

When a client program, such as a web browser, establishes a connection to a destination service, such as a web server, it connects to an application gateway, or proxy. The client negotiates with the proxy server in order to gain access to the destination service. In effect, the proxy establishes the connection with the destination before the firewall and on behalf of the client, hiding and protecting individual computers on the network behind the firewall. This process actually creates two connections. There is one connection between the client and the proxy server and another connection between the proxy server and the destination.

Once a connection is established, the application gateway makes all decisions about which packets to forward. Since all communication is conducted through the proxy server, computers behind the firewall are protected.

With an application gateway, each supported client program requires a unique program for individual user authentication, which makes them quite effective at blocking unwanted traffic. However, a disadvantage is that these firewalls use a lot of system resources. The process of authenticating client applications uses more memory and CPU time than simple packet filtering.