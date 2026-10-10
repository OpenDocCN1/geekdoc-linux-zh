
The scanning techniques described in this section can penetrate a firewall. Many tools are deployed in the security and hacking world, but very few rank higher than scanners.

> In this book, a firewall is defined as a security system intended to protect an organization's network against external threats from another network, such as the Internet. A firewall prevents computers in the organization's network from communicating directly with external computers, and vice versa. Instead, all communication is routed through a proxy server outside of the organization's network; the proxy server determines whether it is safe to let a particular message or file pass through to the organization's network.

Scanners send multiple packets over communication mediums, following various protocols utilizing service ports, then listen and record each response. The most popular scanners, such as nmap, introduced later in this chapter, employ known techniques for inspecting ports and protocols, including:

- **TCP Port Scanning**. This is the most basic form of scanning. With this method, you attempt to open a full TCP port connection to determine if that port is active, that is, "listening."
- **TCP SYN Scanning**. This technique is often referred to as *half-open* or *stealth* scanning, because you don't open a full TCP connection. You send a SYN packet, as if you are going to open a real connection, and wait for a response. A SYN/ACK indicates the port is listening. Therefore, a RST response is indicative of a nonlistener. If a SYN/ACK is received, you immediately send a RST to tear down the connection. The primary advantage of this scanning technique is that fewer sites will log it.
- **TCP FIN Scanning**. There are times when even TCP SYN scanning isn't clandestine enough to avoid logging. Some firewalls and packet filters watch for SYNs to restricted ports, and programs such as Synlogger and Courtney are available to detect these scans altogether. FIN packets, on the other hand, may be able to pass through unobstructed. The idea is that closed ports tend to reply to your FIN packet with the proper RST, while open ports tend to ignore the packet in question.
- **Fragmentation Scanning**. This is a modification of other techniques. Instead of just sending the probe packet, you break it into a couple of small IP fragments. Basically, you are splitting up the TCP header over several packets to make it harder for packet filters to detect what is happening.
- **TCP Reverse Ident Scanning**. As noted by security guru Dave Goldsmith in a 1996 bugtraq post, the ident protocol (RFC 1413) allows for the disclosure of the username of the owner of any process connected via TCP, even if that process didn't initiate the connection. So you can, for example, connect to the http port, then use the ident daemon to find out whether the server is running as root.
- **FTP Bounce Attack**. An interesting "feature" of the FTP protocol (RFC 959) is support for "proxy" FTP connections. In other words, you should be able to connect from evil.com to the FTP server-PI (protocol interpreter) of target.com to establish the control communication connection. You should then be able to request that the server-PI initiate an active server-DTP (data transfer process) to send a file anywhere on the Internet!
- **UDP ICMP Port Unreachable Scanning**. This scanning method varies from the preceding methods in that it uses the UDP protocol instead of TCP. Though this protocol is less complex, scanning it is actually significantly more difficult. Open ports don't have to send an acknowledgment in response to your probe, and closed ports aren't even required to send an error packet. Fortunately, most hosts do send an ICMP_PORT_UNREACH error when you send a packet to a closed UDP port. Thus, you can find out if a port is closed, and by exclusion, determine which ports are open.
- **UDP recvfrom() and write() Scanning**. While nonroot users can’t read port-unreachable errors directly, Linux is cool enough to inform the user indirectly when they have been received. For example, a second write() call to a closed port will usually fail. A lot of scanners, such as ncat and Pluvius’ pscan.c, do this. This is the technique used for determining open ports when nonroot users use -u (UDP).

## Scanner Packages

Many scanners are available to the public, each with its own unique capabilities to perform specific techniques for a particular target. There are TCP scanners, which assault TCP/IP ports and services such as those listed in Chapter 1. Other scanners scrutinize UDP ports and services, some of which were also listed in Chapter 1. This purpose of this section is to identify certain of the more popular scanners and to give a synopsis of their functionality. Chapter 12 introduces a complete internetworking security suite, called TigerSuite, whose evaluation is included on this book’s CD.

### CyberCop Scanner

**Platforms:** Windows NT, Linux

CyberCop Scanner (shown in Figure 5.7), by Network Associates, provides audits and vulnerability assessments combined with next generation intrusion monitoring tools and with advanced decoy server technology to combat snooping. CyberCop examines computer systems and network devices for security vulnerabilities and enables testing of NT and UNIX workstations, servers, hubs, switches, and includes Network Associates’ unique tracer packet firewall test to provide audits of firewalls and routers. Report options include executive summaries, drill-down detail reports, and field resolution advice. One very unique feature of CyberCop Scanner is their auto update technology to keep the kernel engine, resolution, and vulnerability database current. Various forms of reporting analyses are featured such as network mapping, graphs, executive summaries, and risk factor reporting. CyberCop Scanner is certainly among the top of its class in vulnerability scanning today.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_142_0.png)
![](img/ba85bb40c695c02adae8cbd6666f2e0c_143_0.png)

**Hacker's Note** In North America, CyberCop Scanner can be evaluated by clicking on www.networkassociates.com.

### Jakai

**Platform:** Linux

Jakai is among the more popular of the scanners just defined as stealth or half-scan. Recall the communication handshake discussed in Chapter 1: A stealth scanner never completes the entire SYN/ACK process, therefore bypassing a firewall, and becoming concealed from scan detectors. This method allows stealth scanners like Jakai to indiscreetly generate active ports and services. A standard TCP connection is established by sending a SYN packet to the destination host. If the destination is waiting for a connection on the specified port, it responds with a SYN/ACK packet. The initial sender replies with an ACK packet, and the connection is established. If the destination host is not waiting for a connection on the specified port, it responds with an RST packet. Most system logs do not list completed connections until the final ACK packet is received from the source. Sending an RST packet, instead of the final ACK, results in the connection never actually being established, so no logging takes place. Because the source can identify whether the destination host sent a SYN/ACK or an RST, an attacker can determine exactly which ports are open for connections, without the destination ever being aware of the probing. Keep in mind, however, that some sniffer packages can detect and identify stealth scanners, and that detection includes the identity of the scanning node as well.

**Hacker's Note** Jakai can be evaluated on this book's CD.

### NetRecon

**Platform:** Windows NT

NetRecon (shown in Figure 5.8), by Axent, is a network vulnerability assessment tool that discovers, analyzes, and reports vulnerable holes in networks. NetRecon conducts an external assessment of current security by scanning and probing systems on the network. NetRecon re-creates specific intrusions or attacks to identify and report network vulnerabilities, while suggesting corrective actions. NetRecon ranks alongside CyberCop Scanner among the top of its class in vulnerability scanning today.
