should exist where these tests can be performed on staging servers. This ensures that the soon-to-be-rolled-out changes are secure. If not, the tests will generate downtime in the development section, not in production.

# Detecting a Network-based Intrusion

Attackers use application vulnerabilities to gain unauthorized access to systems. We saw in the preceding section how tools such as Nessus help identify vulnerable services and, when possible, recommend ways to remedy the problem. Before attackers can exploit a vulnerable system, they must know it exists.

The following sections examine a number of different methods that can be used to protect a network environment. We also examine techniques that can be used to detect the presence of unwanted guests.

# Know Your Traffic, Tune Your Firewall

Applications and users require a transport mechanism for communicating with each other. In a standard network environment, this is handled by using a number of network protocols such as TCP/IP, ICMP, and UDP. For each of these, applications require predefined ports over which the communications will take place.

The file /etc/services contains a number of well-known, predefined protocol-port pairs and the applications they support. If you know the applications that are being run within your environment, you should be able to generate a list of required ports. /etc/services is a static ASCII file used for referencing ports and applications. It does not prevent the binding of services to any specific port. Restricting network traffic flow to only these select ports will reduce your overall exposure. In addition, a proper review of requirements may identify that some services can be restricted to specific clients. Further constraints can be placed on network flow to allow only these conversations.

As an extra level of complexity, some applications initiate conversations only on a specific port. After the appropriate handshake has been performed, the communications exchange is shifted to a different, sometimes random, port.

When you are finished with the application-port mapping exercise, you will have a list of valid client/server/port relationships that are required to support your applications. Layered on top of the business list of ports is the more transparent layer. Protocols such as DHCP, DNS, and NNTP are often forgotten in the application lists. If they are not included at this step in the process, a number of critical applications may fail. The availability of each of these