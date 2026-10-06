# Appendix A · Answers to Review Questions

networking, option D is incorrect. DHCP functions fine without a gateway, provided a DHCP server is on the same local segment as its clients (as is normally the case), option E is incorrect.

+   4. The Secure Shell (SSH) protocol uses port 22, so the traffic to port 22 is using the correct protocol, is SSH traffic, and option D is correct. The Hypertext Transfer Protocol (HTTP) option bound 80; the Mail Transfer Protocol (SMTP) option uses port 25; Telnet (option C) uses port 22; and the Network News Transfer Protocol (NNTP) option E uses port 119. None of these normally be directed to port 22.

+   5. The Interactive Mail Access Protocol (IMAP) is assigned to TCP port 143. Ports 21, 25, and 110, are all assigned to the File Transfer Protocol (FTP), the Mail Transfer Protocol (SMTP), the Post Office version 3 and the Hypertext Transfer Protocol over SSL (HTTPS). Although some IMAP server programs support POP-3 and might therefore listen to ports 110 and 143, the question specifies IMAP exchanges, so option D is the only answer.

+   6. E, Option D, dhcdpd, is the Linux DHCP server. E, ifconfig can be used for network configuration but is not a DHCP client. The others are all clients. Any given computer will use one DHCP client (or none at all), but from one to three of A, B, and D will be available choices.

+   7. B, When used to display information on an interface, ifconfig shows the hardware and IP addresses (options B and C) of the interface, the protocols (as TCP/IP) bound to the interface, and statistics on transmitted and received packets. This does not return information about programs using the interface (option A), the hostname associated with the interface (option D), or the kernel driver used by the interface (option E).

+   8. The host program (option A) is a commonly used program to perform a DNS lookup. There is no standard nslookup program (option B), although the lookup program for performing DNS lookups, pump (option C) is a DHCP client. ifconfig (option D) is used for configuration of network parameters and cards. netstat (option E) is a general-purpose network diagnostic tool.

+   9. To add a gateway of 192.168.0.1, the command would be add default gw 192.168.0.1, as in specifying the IP address of the host system (as in options A, C, and D) is not necessary and in fact confuse the route command. Although routes provides a -host option using host (without a dash), as in option E, is incorrect. Furthermore, option E edits the critical parameter.

+   10. A, The dhclient utility, if installed, attempts to configure and bring up the network(s) passed to it (or all networks if it) using a DHCP server for guidance. Option A may work, although it won't work if no DHCP server is available. Option B applies whatever network options are configured using distribution-specific tools and brings up the network. Thus, option A and B may both work, although neither is guaranteed to work. Option C displays the network status of eth1, but it won't activate