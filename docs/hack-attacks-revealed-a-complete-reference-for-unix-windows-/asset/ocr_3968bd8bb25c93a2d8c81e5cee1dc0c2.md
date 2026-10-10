# CHAPTER 11

# Proxies and Firewalls

This chapter explores common Underground vulnerability secrets for perimeter protection mechanisms, specifically proxies and firewalls. To review, a proxy is a computer program that acts as a liaison between a user's Web browser and a Web server on the Internet. With this software installed on a server, the proxy is considered a “gateway,” separating the user's internal network from the outside; primarily, it controls the application layer as a type of “firewall,” which filters all incoming packets, and protects the network from unauthorized access. Accordingly, dependable firewall software controls access to a network with an imposed security policy, by means of stateful inspection filters, alternately blocking and permitting traffic to internal network data.

# Internetworking Gateways

To demonstrate the information contained in this chapter, we'll discuss breaches as they pertain to these specific products: BorderWare, Firewall-1, Gauntlet, NetScreen, PIX, Raptor, and WinGate.

# BorderWare

Running on standard Intel platforms, BorderWare (www.borderware.com) uses three perimeter defense software modules for comprehensive network protection. These modules provide packet filtering and circuit-level and application-level gateway monitoring. Other features of the BorderWare firewall include server-to-server and client-to-server VPN access, URL and Web site filtering, and extranet and ecommerce application security. The BorderWare Firewall Console, although somewhat tedious, provides convenient menu-driven administration access to the BorderWare modules. The default firewall configuration prohibits all direct connections from the outside interface to the protected network. As a result, a remote-access component must be configured independently. BorderWare does not come with a command-line administration interface.

# Liabilities

Tunneling

**Synopsis:** Using stealth scanning and/or distorted handshake techniques, a remote attacker can detect ACK tunnel daemon software.

**Hack State:** Unauthorized remote control of target systems.

**Vulnerabilities:** All versions, depending on the configuration.

**Breach:** As explained in previous chapters, TCP establishes virtual connections on top of IP. A session is established when a sender forwards a SYN and the receiver responds with a SYN/ACK. Common packet-filtering firewalls assume that a session always starts with a SYN segment. Therefore, they apply their policies on all SYN segments. Normally, manufacturers develop firewalls to apply these rules to SYNs, rather than to ACKs, because a standard session can contain thousands or millions of ACK segments, while containing only one SYN. This reduces the overall firewall workload and helps to reduce the costs of colossal server requirements. In scenarios such as this,