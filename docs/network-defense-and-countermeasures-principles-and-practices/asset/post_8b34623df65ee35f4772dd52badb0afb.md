
## What Is a Firewall?

- Linksys (www.linksys.com/) makes a number of small office/home office router products that use SPI technologies. These are very inexpensive and easy to configure.
- Cisco (www.cisco.com) is a very well-known and highly respected vendor for many different types of network products, including router firewalls that use SPI technology.

> FYI: Stateless Packet Filtering

Stateful packet inspection is clearly the preferred method. The natural follow-up question is: What about stateless packet filtering? This term is not generally used by security professionals; it merely denotes the standard packet filtering method.

## Application Gateway

An application gateway (also known as application proxy or application-level proxy) is a program that runs on a firewall. This type of firewall derives its name from the fact that it works by negotiating with various types of applications to allow their traffic to pass the firewall. In networking terminology, negotiation is a term used to refer to the process of authentication and verification. In other words, rather than looking at the protocol and port the packet is using, an application gateway will examine the application and the server-side application to which it is trying to connect. It will then determine if particular client traffic is permitted through the firewall. This is significantly different from a packet filtering firewall, which examines the packets and has no knowledge of what sort of application sent them. Application gateways enable the administrator to allow access only to certain specified types of applications, such as web browsers or FTP clients.

When a client program, such as a web browser, establishes a connection to a destination service, such as a web server, it connects to an application gateway, or proxy. The client negotiates with the proxy server in order to gain access to the destination service. In effect, the proxy establishes the connection with the destination before the firewall and on behalf of the client, hiding and protecting individual computers on the network behind the firewall. This process actually creates two connections. There is one connection between the client and the proxy server and another connection between the proxy server and the destination.

Once a connection is established, the application gateway makes all decisions about which packets to forward. Since all communication is conducted through the proxy server, computers behind the firewall are protected.

With an application gateway, each supported client program requires a unique program for individual user authentication, which makes them quite effective at blocking unwanted traffic. However, a disadvantage is that these firewalls use a lot of system resources. The process of authenticating client applications uses more memory and CPU time than simple packet filtering.

## CHAPTER 3 Fundamentals of Firewalls

FYI: Unique Logons

Be aware that having a unique logon for each user is probably the ideal solution for sites with a great deal of public traffic, such as an e-commerce site. On sites such as this, you want to attract a high volume of traffic, mainly from new customers. New visitors to your site will not have a logon ID or password. Making them go through the process of setting up an account to visit your website will likely turn off many potential customers. However, this can be an ideal solution for a corporate network.

Application gateways are also susceptible to various flooding attacks (SYN flood, ping flood, etc.) for two reasons. The first potential cause of a flooding attack may be the additional time it takes for an application to authenticate a request. Remember that both the client application and the user may need to be authenticated. This takes more time than simply filtering packets by certain parameters. For this, a flood of connection requests can overwhelm the firewall, preventing it from responding to legitimate requests. Application gateways may also be more susceptible to flooding attacks once a connection is made, packets are not checked. If a connection is established, then that connection can be used to send a flooding attack to the server it connected to, such as a web server or e-mail server. This vulnerability is mitigated by authenticating users. Provided the user logon method is secure (appropriate passwords, encrypted transmission, etc.), the likelihood that someone can use a legitimate connection through an application gateway for a flooding attack is reduced.

Chapter 4 discusses specific firewall implementations; however, a brief summary of a few application gateway products are provided here:

- Akamai has a robust application gateway, available at https://content.akamai.com/us-en-pg9554-gartner-magic-quadrant.html.
- WatchGuard Technologies offers several firewall solutions (www.watchguard.com/).
- Cloudflare offers an application gateway, specifically a web application firewall: https://www.cloudflare.com/lp/waf-a.

## Circuit Level Gateway

Circuit level gateway firewalls are similar to application gateways but are more secure and generally implemented on high-end equipment. These types of firewalls also employ user authentication, but they do so earlier in the process. With an application gateway, first the client application is checked to see if access should be granted, and then the user is authenticated. With circuit level gateways, authenticating the user is the first step. The user's logon ID and password are checked, and the user is granted access before the connection to the router is established. This means that each individual, either by username or IP address, must be verified before any further communication can take place.

Once this verification takes place and the connection between the source and destination is established, the firewall simply passes bytes between the systems. A virtual "circuit" exists between the internal client and the proxy server. Internet requests go through this circuit to the proxy server, and the proxy server delivers requests to the Internet after changing the IP address. External users only see the IP address of the proxy server. Responses are received by the proxy server and sent back through the circuit to the client. It is this virtual circuit that makes the circuit level gateway secure. The private secure connection between the client application and the firewall is a more secure solution than some other options, such as the simple packet filtering.

## What Is a Firewall?
(Repeated content from OCR flow)

## Application Gateway
(Repeated content from OCR flow)

## Circuit Level Gateway
(Repeated content from OCR flow)

## CHAPTER 3 Fundamentals of Firewalls
(Repeated content from OCR flow)

## Hybrid Firewalls
(Repeated content from OCR flow)

## Blacklisting/Whitelisting
(Repeated content from OCR flow)

## Implementing Firewalls
(Repeated content from OCR flow)

## Host-Based
In the host-based (sometimes called network host-based) scenario the firewall is a software solution installed on an existing machine with an existing operating system. The most significant concern in this scenario is that, no how good the firewall solution is, it is contingent upon the underlying operating
