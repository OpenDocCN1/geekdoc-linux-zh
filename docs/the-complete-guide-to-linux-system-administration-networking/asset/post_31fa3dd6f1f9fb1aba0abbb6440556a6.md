
| Command | Description | Example |
|---|---|---|
| system-config-securitylevel-tui | Text and menu-based utility for configuring an overall security level in Red Hat Linux and Fedora | system-config-securitylevel-tui |
| tcpd | The daemon that implements TCP Wrappers | tcpd in.ftpd |
| tcpdump | Command-line network traffic analysis utility | tcpdump |
| ethereal | Text-based program similar to Ethereal, used to display and analyze the contents of network packets; a packet sniffer | ethereal |
| tkman | Graphical display tool for man pages (not included in Red Hat Linux and Fedora) | tkman bash |
| usbmodules | Information and configuration tool for USB devices | usbmodules |
| whois | A utility that queries an Internet database to learn about the person who manages a specific domain | whois www.law.gw.edu |
| xauth | A security system for managing display of graphical programs on remote computers by sharing a numeric token called a cookie; also the program used in Linux to manage this security system and the numeric cookies associated with it | xauth |
| xfontsel | Graphical program that displays available fonts in the X Window System and lets you select the default font to use for title bars, menus, etc. | xfontsel |
| xhost | A program that can control access by X clients to an X server for display of graphical programs; xhost is not a secure system | xhost + |
| xinetd | A superserver with extended configuration options; standard on Red Hat Linux instead of the more usual inetd program | xinetd |
| xinfo | Graphical display tool for info pages (not included in Red Hat Linux and Fedora) | xinfo ls |
| xinit | Program that starts the X server; called by the startx script | xinit |
| xman | Graphical display tool for man pages (not included in Red Hat Linux and Fedora) | xman nmap |
| xrdb | Manages X resource database information for graphical programs | xrdb -load $HOME/.Xresources |
| xset | Sets options within the X Window System | xset s noblank |
| xvidtune | Graphical utility that adjusts display characteristics of the X Window System | xvidtune |

## Key Terms

.forward — Configuration file placed in a user's home directory to define where e-mail messages should be forwarded by sendmail.

.Xauthority — Configuration file containing tokens (cookies) used by the xauth program to enable remote display of graphical programs.

/etc/exports — File containing a description of local file systems and directories to be made available using NFS.

/etc/hosts.allow — Configuration file that defines services and hosts that should be permitted access by TCP Wrappers.

/etc/hosts.deny — Configuration file that defines services and hosts that should be denied access by TCP Wrappers.

/etc/nologin — A file whose existence prevents all users except root from logging in to the system. Regular users attempting to log in see the contents of the file /etc/nologin.

/etc/securetty — Configuration file that lists locations from which root is permitted to log in. Used to prevent root from logging in via a remote connection, such as a modem.

/etc/services — Configuration file that maps service names to port numbers. Used by many programs, including the superservers inetd and xinetd.

Access Control Lists (ACLs) — Data structures that define who can access individual directories and programs.

Apache — A popular Web server program.

Apache modules — Program code that can be loaded independently into the Apache Web server.

background application — An application that does not prevent the program that started it from immediately interacting further with the user.

buffer overflow attack — A technique for gaining access to a computer system by exploiting a weakness in the design of a computer program. When a cracker follows a specific sequence of steps or provides specific input to a program, the program becomes confused and tries to use computer memory inappropriately; consequently, the buffer, or memory space, reserved for a part of the program overflows. The result can be either corruption of system data, a crashed server, or even direct root access.

**caching name server** — A DNS server that contains no preconfigured information on domains (except localhost), but simply queries other DNS servers and caches the results.

**CERT Coordination Center (CERT/CC)** — A federally funded software-engineering institute that focuses much attention on computer security issues and provides information to security and system administration professionals around the world; operated by Carnegie-Mellon University.

**container** — A special type of Apache configuration directive that activates other directives only if a condition is met or only within a particular context.

**cookie** — A numeric token used by a program to identify information about a host or user.

**denial of service (DoS)** — A cracker activity that ties up the attacked server or a particular program with so much bogus network traffic that it cannot respond to valid requests.

**distributed DoS (DDoS)** — A special type of denial-of-service attack in which a cracker infiltrates many systems and installs a program that executes a DoS attack on an assigned target at the cracker’s command.

**e-mail alias** — An alternative name that can be used to e-mail messages to a user account.

**Ethereal** — A powerful graphical network traffic analysis tool.

**firewall** — A program that filters (blocks) IP packets based on their characteristics and according to a set of rules.

**gdm** — The display manager included with GNOME; used to provide a graphical login prompt.

**Global Information Assurance Certification (GIAC)** — A hands-on security certification program run by the SANS Institute.

**hard mount** — A method of mounting an NFS file system in which programs will wait—without limit—for the NFS server to respond.

**intrusion detection system (IDS)** — A type of software that aids network intrusion detection.

**IP chains** — An older packet-filtering (firewalling) technique used in the Linux kernel.

**IP masquerading** — A type of network address translation in which packets from many computers on a LAN are altered to appear as if they came from a single computer.

**IP tables** — The lists of rules associated with one of the programming hooks provided in the networking stacks by the NetFilter architecture.

**kdm** — The display manager included with KDE; used to provide a graphical login prompt.

**Linux Intrusion Detection System (LIDS)** — A complex intrusion detection system that alters the Linux kernel to remove root’s comprehensive access to a Linux system.

**Mail Delivery Agent (MDA)** — A program that places e-mail in a user’s mailbox so that it can be read. This function is often subsumed by an MTA.

**Mail Transfer Agent (MTA)** — A program that moves e-mail messages from one server on the Internet to another. Also called an e-mail server.

**Mail User Agent (MUA)** — A program that displays and manages e-mail messages for a user.

**map** — A technique in which user account information for an incoming client request is assigned to a user account on the server that processes that request.

master DNS server — The authoritative name server for a zone, typically containing database files that provide IP addresses for hosts within that zone.

metaserver — See superserver.

MIT Magic Cookie — The name given to a cookie used by the xauth program for X display authentication.

NetFilter — The packet-filtering and advanced routing architecture in Linux 2.4 and 2.6 kernels.

network address translation (NAT) — A routing technique in which the addresses or other header information in a packet is altered during routing.

Network File System (NFS) — A network service that permits remote users to mount and work with a file system as part of their directory structure.

network traffic analysis — See packet sniffing.

packet filter — A technique in which network packets are processed according to their contents, usually based on a series of rules that compose a firewall. Handled in the Linux kernel using rules defined by the iptables command.

packet sniffing — A network activity in which the headers and payload of all packets on the network are captured and examined (also called network traffic analysis).

password cracking — A cracker activity by which the cracker obtains the password for a valid user account, either by using a program that examines millions of passwords until the correct one is found, or by guessing based on personal knowledge about the user.

port — A number that is associated with a network-capable application.

port scanning — A network activity in which packets sent to a host are analyzed to learn about that host.

primary DNS server — See master DNS server.

proxy server — A server that receives a client request that is intended for a different server. The proxy server then makes the request as if the proxy server itself were the client; when the intended server responds, the proxy server sends the response to the client.
