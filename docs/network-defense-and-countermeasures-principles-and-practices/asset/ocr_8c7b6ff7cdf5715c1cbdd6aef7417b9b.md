# CHAPTER 2 Types of Attacks

The danger from IP spoofing is that some firewalls do not examine packets that appear to come from an internal IP address. Routing packets through filtering routers is possible if they are not configured to filter incoming packets whose source address is in the local domain.

Examples of router configurations that are potentially vulnerable

+   - Routers to external networks that support multiple internal interfaces
- Proxy firewalls where the proxy applications use the source IP address for authentication
- Routers with two interfaces that support subnetting on the internal network
- Routers that do not filter packets whose source address is in the local domain

The best method of preventing IP spoofing is to install a filtering router. Filtering routers incoming packets by not allowing a packet through if it has a source from your internal network, you should filter outgoing packets that have a source address different from your internal network to prevent a source IP spoofing attack originating from your site. Many commercial firewall vendors, such as Cisco, FortGate, D-Link, and Juniper, use this option.

If your router does not support filtering on the inbound side of the interface and you feel the need to immediately filter the spoofed IP packets by using a second router between your external interface and your outside connection. Configure this router to block, the outgoing interface connected to your original router, all packets that have a source address in your internal network. For this purpose, you can use a filtering router or a Unix system with two interfaces that supports packet filtering.

# Defending Against Session Hijacking

Another form of attack is session hacking or hijacking. TCP session hijacking is a process whereby a hacker takes over a TCP session between two machines. Because authentication is frequently done only at the start of a TCP session, this allows the hacker to break into the communication stream and take control of the session. For example, a person might log on to a machine remotely. After she has established a connection with the host, the hacker might use session hacking to take over that session and thereby gain access to the target machine.

One popular method for session hacking is using source-routed IP packets. This allows a hacker at point A on the network to participate in a conversation between B and C by encouraging the IP packets to pass through the hacker's machine.

The most common sort of session hacking is the “man-in-the-middle attack.” In this scenario hacker uses some sort of packet-sniffing program to simply listen in on the transmissions between two computers, taking whatever information he or wants but not actually disrupting the conversation.