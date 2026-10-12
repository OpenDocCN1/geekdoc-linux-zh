know what it was doing) In practice, a well-administered simple firewall is much more secure than a badly configured sophisticated system that nobody understands.

+   9. if the firewall will be performing authentication, e.g. for users connecting via dial-up ISPs over the Internet, does the firewall support LDAP for accessing user databases? Does it support any other user-database management tools you might want (e.g. integration with your Windows-NT domains or Active Directory)?

+   10. what type of logging and reporting does it support? Can it use syslog to integrate its logs with the rest of your log-handling infrastructure? Does it integrate with third-party log analysis and reporting tools? Does it give full usage reporting or just exception reports? Can it alert you when it detects that you are being attacked? (See also Intrusion Detection Systems, Module 25.1.)

+   11. for small networks, having a 4- or 8-port UTP hub, and/or a DHCP server built into the firewall can be convenient.

# Dedicated hardware appliance, or software firewall on a PC?

In our experience, dedicated hardware firewall appliances are often a better option than a firewall software package running on a standard PC or workstation:

+   - we've found that appliance firewalls are much easier to set up and to manage

+   - they save you the cost of a machine to run the software on

+   - they avoid a lot of the operating system (O/S) bugs and configuration problems that can affect software firewalls. As we said earlier, the more code you have, the more bugs you have, and NT and Linux are huge. You have to know what you're doing and *harden the O/S*, by removing as much as possible and modifying your configurations specially for security (see Notes). Appliances have a tiny O/S and no extra applications so they minimize the risks.

# Performance considerations

+   12. can the firewall handle the throughput (Mb/s) of the Internet connection you are using, for normal (unencrypted) traffic and for VPN (Chapter 27) if you are going to use it?

+   13. how many simultaneous connections can the firewall handle? This is important for busy sites. Small sites could easily be handled within the 5000 connection limit of a small to medium-sized firewall, whereas large, busy, or e-commerce sites might need hundreds of thousands of connections

+   14. what speed are the Ethernet interfaces: 10Mb/s, 100Mb/s, or 1Gb/s? While most sites don't have an Internet connection anywhere near 10Mb/s, you may still want faster Ethernet if, for example, you have a Web server running on the DMZ, pulling a large amount of data from database servers on the LAN. On a general-purpose computer used as a firewall you can change you Ethernet cards to suit your network, but if you need a 1Gb/s card, be sure that the computer you're using can deliver the throughput you need.