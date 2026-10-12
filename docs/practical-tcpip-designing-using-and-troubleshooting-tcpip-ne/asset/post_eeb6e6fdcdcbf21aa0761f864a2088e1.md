
## 24.4 Stateful packet inspection and resource usage

Let's look at a specific example of how an SPI firewall can block a particular type of attack, using its state information. A common denial of service (DoS) attack is the “SYN Flood.” Here's how it works. When a TCP connection is being established, client and server go through the normal SYN, SYN/ACK, ACK three-way handshake (Module 10.8). When the server receives the initial SYN from the client, it replies with SYN/ACK and creates an entry in an internal table saying it's awaiting an ACK from the client to complete the connection establishment (Figure 24.5).

![](img/a2132b646d336d5f9a21102d6320e537_661_0.png)

Figure 24.5 Server awaiting an ACK to complete connection establishment

When the client sends the answering ACK, the server removes the entry from the “awaiting ACK” table because the connection is now fully established (Figure 24.6).

![](img/a2132b646d336d5f9a21102d6320e537_661_1.png)

Figure 24.6 Connection established — three-way handshake completed

In a SYN flood, the attacker sends a large number of SYNs in quick succession and never completes the connection establishment. The server's internal table fills up (Figure 24.7) so it's unable to accept connections from any other, real clients. In this way it has denied service to legitimate users.

SPI firewalls can protect servers from this type of attack. Instead of passing the initial SYN through to the server, the firewall itself sends the SYN/ACK, and awaits the establishing ACK. If the client is legitimate and sends the ACK, the firewall then performs its own three-way handshake with the server (Figure 24.8); when that's complete, it passes all traffic from the legitimate client to the server as normal. However, if the client is a hacker attempting a SYN flood, the real server is never contacted; the firewall detects the attack, recognizing the abnormal load of incomplete connection establishments and discarding them. The firewall may also raise an alert to inform the network manager of the attack.

![](img/a2132b646d336d5f9a21102d6320e537_662_0.png)

Figure 24.7 Internal table fills up

![](img/a2132b646d336d5f9a21102d6320e537_662_1.png)

Figure 24.8 Firewall's three-way handshake with the server

Because the firewall must maintain state tables for each established TCP connection, for connections in the process of being established, and for UDP and ICMP packets, it can use a lot of memory. This is why you will often see a firewall advertised as “handling 5000 simultaneous connections” or similar. The busier your site, the more connections will be needed, so the firewall must have the memory and processing power to handle the likely volume.

## 24.5 How firewalls work (3) – application-level gateways

An application-level gateway (ALG) is a firewall program that runs at the application level of the TCP/IP stack, not at the IP packet level. ALGs are also called application proxies or application-level proxies. Figure 24.9 shows a client on the Internet connecting to one of our internal servers via an ALG firewall.

![](img/a2132b646d336d5f9a21102d6320e537_663_0.png)

Figure 24.9 Separate TCP connections on either side of ALG firewall

- the client establishes a connection to the ALG
- the ALG connects to the server
- the ALG acts as a proxy on behalf of the client. It accepts requests from the client, analyzes them, and if they are acceptable according to the firewall's rules, re-issues them on the ALG's connection to the server. The ALG handles responses from the server in the same way.

With an ALG there are two separate TCP connections, as illustrated in Figure 24.9. This is fundamentally different from packet filter and stateful packet inspection firewalls where there is a single connection – from the client to the server – with the firewall acting almost as a router (Figure 24.10).

![](img/a2132b646d336d5f9a21102d6320e537_663_1.png)

Figure 24.10 Non-ALG firewall acts almost as a router

With the ALG, packets from the client are not forwarded to the server – only the semantic information (protocol commands, etc.) extracted from the packets is relayed. Malformed packets sent from the client – either because of a faulty client implementation or because they are deliberately malformed as part of a hacker attack – can never reach the server.

### Advantages of application-level gateway firewalls

- ALGs understand the application-level protocols being used, so they can check the meaning of requests and replies. Let's take some examples:
  - an early version of the sendmail mail server had a “backdoor” built in for debugging: if you used the WIZ (wizard) command, you could get root user (administrator) access. Because packet filters and SPI firewalls don’t understand the SMTP protocol at this high level, they can’t block valid but unwanted commands like this. Because the ALG does operate at the application level, it can easily block this type of request
  - ALGs can offer fine control over requests sent to a Web server. At the simplest level, the firewall could block certain URLs when requested by certain internal IP addresses. It could also block the Code Red worm’s requests: they are valid according to the HTTP specs, but are recognizable because of the particular URL they request
  - you could allow FTP GET requests but block PUT requests, so Internet users can retrieve files from your FTP server but can’t deposit virus-laden or other troublesome files.
- ALGs can give very detailed, protocol-specific logging.

### Disadvantages of application-level gateway firewalls

- because of the amount of state information and the number of open connections they maintain, ALGs need more memory and processing power than packet filters or SPI firewalls. They may also be slower because of the extra load of extracting and validating the application-level semantics
- a separate proxy application must be provided within the firewall for each different protocol supported. When a new protocol or service is developed, there will usually be a delay before the firewall manufacturer releases a suitable proxy. For most people this delay won’t matter, and anyway a generic proxy application can often be used as a stop gap. This will have no specific knowledge of the new protocol, but will allow it to operate through the firewall. Proxy programs are often only a few hundred lines of C program code, so they can be produced quickly
- (some old ALGs and proxies only worked with special versions of client applications or libraries that were aware they were using the ALG, but nowadays most ALGs are “transparent” giving the illusion that the client is connected directly to the server, and don’t need any special client software.)

### Hybrid firewalls

Hybrid firewalls are a mixture of stateful packet inspection for performance, and ALGs for fine control of specific protocols. Many modern firewalls are hybrids of this type.

If your firewall doesn’t contain some ALG-like functionality, especially for e-mail and Web traffic, you should consider a separate security tool (program or appliance) to give you finer control (Chapter 25).

## 24.6 Using a demilitarized zone (DMZ) on a firewall

A *demilitarized zone* (DMZ) is a half-way-house network between the untrusted, external Internet and your trusted, internal LAN. It contains servers that are accessible from the Internet, e.g. the e-mail server that receives messages from the Internet, and the Web server that hosts your public Web site (Figure 24.11). The firewall allows outsiders on the Internet to access the servers on the DMZ but not any machines on your LAN.

![](img/a2132b646d336d5f9a21102d6320e537_665_0.png)

Figure 24.11 Demilitarized zone on a firewall for publicly-accessible servers

The purpose of a DMZ is to keep your public servers completely separate from your private LAN, in case the public servers are compromised. "Compromised?" you ask, horrified. "Does that mean the firewall doesn't give me 100% protection?" The answer is the one you really didn't want to hear: no firewall is 100%. Accepting that fact helps you secure your systems by encouraging you to take the approach, "OK, that protects us from ABC, but what if XYZ happens after that? Can we put in a second or third line of defense?" (This is called "security in depth.")

To protect your LAN, the firewall restricts traffic from DMZ to LAN, as well as from WAN to LAN. Then, if your Web server, say, is broken into, your LAN is still protected, because the intruder still has to go through the firewall to reach the LAN. But if your Web server lived on the LAN instead, and was broken into, the intruder would have a clear run from the Web server to everything else on your network. You *do* have to plan for this type of intrusion: e-mail and Web servers are notorious for having security holes in them.

Even though some access to the DMZ is allowed from the Internet, it is good practice to configure the firewall as restrictively as possible. Allow access only to the specific services you want to be accessible -- HTTP and SMTP on a typical site -- and block everything else. This accords with another general security principle: allow nothing at all initially, and then only open up as little as possible. This approach helps protect you from inadvertent misconfigurations. For example, let's assume your Web server is a Windows machine and it's running Microsoft Windows Networking. If the firewall allows access to this server, a hacker could
