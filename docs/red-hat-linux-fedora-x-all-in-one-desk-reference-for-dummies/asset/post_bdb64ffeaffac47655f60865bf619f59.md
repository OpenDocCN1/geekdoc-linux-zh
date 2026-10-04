
## 568 Setting Up Simple Firewalls

![](img/d9230b719dc0efd80851f363d8c6f571_594_0.png)

The dual-homed host is turned into a firewall by running application gateways — proxy services — on the dual-homed host. These proxy services allow specific applications, such as FTP and HTTP, to work across the dual-homed host. That means you can configure the firewall so that internal clients (on the internal network) are able to access Web and FTP servers on the Internet.

Your Public Web site can also run on the dual-homed host and be accessible to everyone on the Internet.

> WARNING! Don't allow user logins on the dual-homed host. Anyone logged into the host can have access to both the internal network and the Internet. Because the dual-homed host is your only barrier between the Internet and the internal network, not increasing the chances of a break-in is best by allowing users to log in to the firewall. Putting user accounts increases the chance of an intruder gaining access to the firewall by cracking a user's password.

## Perimeter network with bastion host

An Internet firewall is often more complicated than a single dual-homed host that connects to both the Internet and the protected network. In particular, if you provide a number of Internet services, you may need more than one system to host them. Imagine you have two systems: one to run the Web and FTP servers and the other to provide mail (SMTP) and domain name system (DNS) lookups. In this case, you place these two systems on a network that sits between the Internet and the internal network. Figure 3-3 illustrates

![](img/d9230b719dc0efd80851f363d8c6f571_595_0.png)

In this case, the firewall includes a perimeter network that connects to the Internet through an exterior router. The perimeter network, in turn, connects to the internal network through an interior router. The perimeter network has one or more hosts that run Internet services, including proxy servers (about which we have a moment) that allow internal hosts to access Web servers on the Internet.

The term bastion host refers to any system on the perimeter network, because such a system is on the Internet and has to be well fortified. The dual-homed host is also a bastion host because the dual-homed host is also accessible from the Internet and has to be protected.

In the firewall configuration shown in Figure 3-3, the perimeter network is known as a DMZ (demilitarized zone) network because network acts as a buffer between the Internet and the internal network (just as a real-life DMZ is a buffer between North and South Korea).

Usually, you combine a packet-filtering router with a bastion host. Your Internet Service Provider typically provides the external router, which means you don't have much control over router's configuration. But you provide the internal router, which means you can choose a screening router and employ some packet-filtering rules. For example, you might employ the following packet-filtering rules:

- From the internal network, allow only packets addressed to the bastion host.
- From the DMZ, allow only packets originating from the bastion host.
- Block all other packets.

These rules ensure that the internal network communicates only with the bastion host (or hosts).

Like the dual-homed host, the bastion host also runs an application gateway that provides proxy services for various Internet services, such as TELNET, FTP, SMTP, and HTTP.

## Application gateway

The bastion host or the dual-homed host is the system that acts as the intermediary between the Internet and the protected internal network. As such, that system serves as the internal network's gateway to the Internet. Toward this end, the system runs software to forward and filter TCP/IP packets for various services, such as TELNET, FTP, and HTTP. The software for forwarding and filtering TCP/IP packets for specific applications are known as proxy servers. Figure 3-4 illustrates a proxy server's role in a firewall.

A proxy server accepts a connection for a specific protocol, such as FTP, and forwards the request to another server. In other, the proxy server acts as a proxy for an actual server. Because it acts as a gateway for a specific application (such as HTTP or FTP), a proxy server is also known as an application gateway.

Figure 3-4: A proxy server lets internal hosts access Internet servers.

![](img/d9230b719dc0efd80851f363d8c6f571_596_0.png)

## Enabling Packet Filtering on Your Fedora Core System

Unlike a screening router, which blocks packets only on the basis of information in the packet header (such as source and destination IP addresses), a proxy server uses the user's data to decide what to do. For example, a proxy server does not blindly forward packets to an Internet service. A proxy server can enforce a site's security policy and allow certain operations, depending on the specific application. For example, an FTP proxy server may prevent users from internal networks from using the FTP command to send files to the Internet.

Accessing an Internet service through a proxy server can be a bit more involved than accessing service directly. For example, a user on the internal network establishes a TELNET session with an Internet host with the following steps:

- 1. The user establishes a TELNET session with the firewall — the system that runs the TELNET.
- 2. The user establishes a TELNET session with the firewall — the system that runs the TELNET.
- 3. The user establishes a TELNET session with the firewall — the system that runs the TELNET.

Besides acting as a gateway, the proxy also logs the accesses. The exact steps you access services through a firewall depend on the client program.

## Enabling Packet Filtering on Your Fedora Core System

Your Fedora Core system comes with built-in packet-filtering software in form of something called netfilter that's in the Linux kernel. All you have to do is use the iptables command to set up the rules for what happens to the packets based on the IP addresses and network connection type.

| Book VII |
|---||
| Chapter 3 |
| Securing Network |

## Enabling Packet Filtering on Your Fedora Core System

The built-in packet-filtering capability is handy when you don't have a dedicated firewall between your Fedora Core system and the Internet. This is the case, for example, when you connect your Fedora Core system to the Internet through a DSL or cable modem. You can essentially have a packet-filtering firewall inside your Fedora Core system, sitting between the kernel and the applications.

### Using the security level configuration tool

You can run on different levels of packet filtering through the graphical Security Level Configuration tool. To run the tool, log in as root and select Main Menu->Settings->Security Level. The Security Level Configuration window appears (see Figure 3-5).

![](img/d9230b719dc0efd80851f363d8c6f571_598_0.png)

From the Security Level drop-down (refer to Figure 3-5), you can select two predefined levels of simple firewall (more precisely, packet filtering) with the Security Level Configuration tool:

- **Disable Firewall:** Does not perform any filtering, and all connections are allowed (you can still turn off Internet services by not running the servers or disabling them in the xinetd configuration files). This security level is fine if your Fedora Core system is inside a protected area network or if you have a separate firewall device.
- **Enable Firewall:** Turns on packet filtering. You can then select the services that you want to allow and the network devices that you trust.
