# ## Defenses

The primary purpose for deploying SSH is security. SSH defends against several attacks that plague IP (Internet Protocol) version 4 networks, including poor protocols with IPv4, such as Address Resolution Protocol (ARP), Initial Sequence Numbers (ISN), and various clear-text protocols, such as Telnet, RSH, Rlogin, FTP, POP3, IMAP, LDAP, and HTTP.

Because space is limited, *Implementing SSH* does not discuss in detail *all* types of attacks that SSH defends against. You should be aware of three critical types of security attacks against which SSH is quite effective. (Be aware that while SSH cannot prevent all of these attacks, it has safeguards in place that make it extremely difficult, if not well-nigh impossible, to execute them.) The three major types of security attacks are:

+   - **Man-in-the-Middle (MITM) attacks.** Man-in-the-Middle attacks occur against ARP in IPv4 networks. Such attacks allow an unauthorized entity to sniff the network even on a switched environment by capturing the communication between two trusted entities. SSH version 2 prevents attackers from gaining access to communication by fully encrypting it. The chances that an attacker can capture the communication between two entities are minimized, as the communication is in a form that is unreadable to the attacker.

+   - **Session hijacking.** Session-hijacking attacks occur against the ISN in the TCP header of a TCP/IP packet. An attacker can take advantage of the poor sequence numbers used by the ISN and hijack a session between two trusted entities. SSH can make it virtually impossible for an attacker to view, capture, or attempt to hijack the ISN altogether, although it can-not always make the ISN in a TCP header less predictable.

+   - **Sniffing.** Sniffing is the simple act of viewing the communication (packets) in a network. SSH provides a strong level of encryption that can protect weak protocols such as Telnet, RSH, Rlogin, FTP, POP3, IMAP, LDAP, and HTTP either by replacing them altogether (for Telnet, RSH, and Rlogin, for example) or by wrapping them within a tunnel (for POP3). This encryption prevents most, if not all, unauthorized users from sniffing the network.

# ## How This Book Is Organized

This book is organized into three main parts: SSH Basics, Remote Access Solutions, and Protocol Replacement. Part One covers the basics of SSH. Chapter 1