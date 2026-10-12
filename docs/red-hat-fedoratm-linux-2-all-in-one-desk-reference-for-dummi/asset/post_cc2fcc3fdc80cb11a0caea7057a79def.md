
These rules ensure that the internal network communicates only with the bastion host (or hosts).

Like the dual-homed host, the bastion host also runs an application gateway that provides proxy services for various Internet services, such as TELNET, FTP, SMTP, and HTTP.

## Application gateway

The bastion host or the dual-homed host is the system that acts as the intermediary between the Internet and the protected internal network. As such, this system serves as the internal network's gateway to the Internet. Toward this end, the system runs software to forward and filter TCP/IP packets for various services, such as TELNET, FTP, and HTTP. The software for forwarding and filtering TCP/IP packets for specific applications are known as *proxy servers*. Figure 3-4 illustrates a proxy server's role in a firewall.

![](img/9f89727199836b0f871f1745838aa8b2_596_0.png)

A *proxy server* accepts a connection for a specific protocol, such as FTP, and forwards the request to another server. In other words, the proxy server acts as a proxy for an actual server. Because it acts as a gateway for a specific application (such as HTTP or FTP), a proxy server is also known as an *application gateway*.

Unlike a screening router, which blocks packets only on the basis of information in the packet header (such as source and destination IP addresses), a proxy server uses the packet's data to decide what to do. For example, a proxy server does not blindly forward packets to an Internet service. The proxy server can enforce a site's security policy and disallow certain operations, depending on the specific application. For example, an FTP proxy server may prevent users from internal networks from using the FTP put command to send files to the Internet.

Accessing an Internet service through a proxy server can be a bit more involved than accessing that service directly. For example, a user on the internal network establishes a TELNET session with an Internet host with the following steps:

- 1. The user establishes a TELNET session with the firewall host — the system that runs the TELNET proxy. To establish a session, the user has to enter a username and password so that the firewall host can verify that the user has permission to connect to the Internet.
- 2. The user enters a command (which the TELNET proxy accepts) to connect to the Internet host. The TELNET proxy, in turn, establishes a TELNET connection between itself and the Internet host.
- 3. The TELNET proxy on the firewall begins passing packets back and forth between the Internet host and the user's system (until the user ends the TELNET session with the Internet host).

Besides acting as a gateway, the TELNET proxy also logs the user's session with the Internet host. The logging is part of an application gateway's security feature because the log file keeps track of all firewall accesses (as well as attempted accesses that may fail because of a wrong username or password).

Although the TELNET session involves two steps — first TELNET to the firewall host and then connect to the Internet host — the process of accessing services through a proxy need not be too cumbersome. The exact steps you take to access services through a firewall depend on the proxy software and the client program you use to access a service. With the right client program, proxies can be transparent to the user. For example, many Web browsers make accessing a Web site through an HTTP proxy easy. All you have to do is indicate through a menu choice the HTTP proxy you want to use.

## Enabling Packet Filtering on Your Fedora Core System

Your Fedora Core system comes with built-in packet-filtering software in the form of something called netfilter that's in the Linux kernel. All you have to do is use the iptables command to set up the rules for what happens to the packets based on the IP addresses in their header and the network connection type.

Book VII
Chapter 3

Securing the
Network

The built-in packet-filtering capability is handy when you don’t have a dedicated firewall between your Fedora Core system and the Internet. This is the case, for example, when you connect your Fedora Core system to the Internet through a DSL or cable modem. You can essentially have a packet-filtering firewall inside your Fedora Core system, sitting between the kernel and the applications.

### Using the security level configuration tool

You can turn on different levels of packet filtering through the graphical Security Level Configuration tool. To run the tool, log in as root and select Main Menu > System Settings > Security Level. The Security Level Configuration window appears (see Figure 3-5).

![](img/9f89727199836b0f871f1745838aa8b2_598_0.png)

From the Security Level drop-down menu (refer to Figure 3-5), you can select two predefined levels of simple firewalling (more precisely, packet filtering) with the Security Level Configuration tool:

- **Disable Firewall:** Does not perform any filtering, and all connections are allowed (you can still turn off Internet services by not running the servers or disabling them in the `xinetd` configuration files). This security level is fine if your Fedora Core system is inside a protected local area network or if you have a separate firewall device.
- **Enable Firewall:** Turns on packet filtering. You can then select the services that you want to allow and the network devices that you trust.

You can allow incoming packets meant for specific Internet services such as SSH, TELNET, and FTP. If you select a network interface such as eth0 (the first Ethernet card) as trusted, all network traffic over that interface is allowed without any filtering.

### Using the iptables command

Using the iptables command is somewhat complex. iptables uses the concept of a chain, which is a sequence of rules. Each rule says what to do with a packet if the header contains certain information (such as the source or destination IP address). If a rule does not apply, iptables consults the next rule in the chain. By default, there are three chains:

- **INPUT:** The first set of rules against which packets are tested. The packets continue to the next chain only if the input chain does not specify DROP or REJECT.
- **FORWARD:** Contains the rules that apply to packets attempting to pass through this system to another system (for example, when you use the Fedora Core system as a router between your LAN and the Internet).
- **OUTPUT:** Includes the rules applied to packets before they are sent out (either to another network or to an application).

You can add rules to these chains or create new chains of rules by using the iptables command. You can also view the current chains and save them to a file. For example, if you do nothing else, the iptables -L command shows the following:

```
Chain INPUT (policy ACCEPT)
target     prot opt source                destination

Chain FORWARD (policy ACCEPT)
target     prot opt source                destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source                destination
```

In this case, all three chains — INPUT, FORWARD, and OUTPUT — show the same ACCEPT policy, which means everything is wide open.

If you’re setting up a packet filter, the first thing you do is specify the packets that you want to accept. For example, to accept packets from the 192.168.0.0 network, add the following rule to the input chain:

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

Now add a rule to drop everything except local loopback (the lo network interface) traffic and stop all forwarding with the following commands:

```
iptables -A INPUT -i ! lo -j REJECT
iptables -A FORWARD -j REJECT
```

![](img/9f89727199836b0f871f1745838aa8b2_599_0.png)

![](img/9f89727199836b0f871f1745838aa8b2_599_1.png)

![](img/9f89727199836b0f871f1745838aa8b2_599_2.png)

The first iptables command, for example, appends to the input chain (-A INPUT) the rule that if the packet does not come from the lo interface (-i ! lo), iptables rejects the packet (-j REJECT).

Before rejecting all other packets, you may also add more rules to each INPUT chain to allow specific packets in. You can select packets to accept or reject based on many different parameters such as IP addresses, protocol types (TCP, UDP), network interface, and port numbers.

![](img/9f89727199836b0f871f1745838aa8b2_600_0.png)

Don't type iptables commands from a remote login session. A rule that begins denying packets from all addresses can also stop what you type from reaching the system; once that happens, you may have no way of accessing the system over the network. To avoid unpleasant surprises, always type iptables rules at the console — the keyboard and monitor connected directly to your Fedora Core PC that is running the packet filter. If you want to delete all filtering rules in a hurry, you can flush them by typing the following command:

```
iptables -F
```

I don't provide all the details of the iptables commands in this section. Sufficient to say that you type man iptables to read a summary of the commands. You can also read about netfilter and iptables at www.iptables.org.

After you define the rules by using the iptables command, they are in the memory and are gone when you reboot the system. To save them, use the iptables-save command to store the rules in a file. For example, you can save the rules in a file named iptables.rules by using the following command:

```
iptables-save > iptables.rules
```

Here's a listing of the iptables.rules file, generated on a Fedora Core system:

```
# Generated by iptables-save v1.2.9 on Wed Apr 14 20:56:40 2004
*filter
:INPUT ACCEPT [44:2024]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [2572:1426880]
-A INPUT -s 192.168.0.0/255.255.255.0 -j ACCEPT
-A INPUT -i lo -j REJECT --reject-with icmp-port-unreachable
-A FORWARD -j REJECT --reject-with icmp-port-unreachable
COMMIT
# Completed on Wed Apr 14 20:56:40 2004
```
