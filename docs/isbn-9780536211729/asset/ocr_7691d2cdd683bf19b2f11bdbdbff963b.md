+   telnet (23/tcp), smtp (25/tcp), dns (53/tcp), pop-3 (110/tcp), snmp (111/udp/tcp), imap (143/tcp), snmp (161/udp), route (520/udp), and mount (635/udp) are favorite target ports. They represent some of the most potentially vulnerable openings to a system, which intrinsically, to common configuration errors, or due to known flaws in the software. Because these services are so common, they are good examples of why you want neither offer them to the outside world, or very carefully offer them with controlled access to these services.

+   NetBIOS (137-139/tcp/udp), SMB on Windows 2000/2003 (445/tcp), Netbus (12345/tcp), and older Back Orifice (31337/udp) probes are notoriously common. They pose no threat to a Linux system. The target is a Windows system, in this case, the scans are all too common not due to the popularity of Windows as a server on the Internet (Linux/Apache is the most popular web server), but rather to the relative insecurity of Microsoft Windows.

# HISTORICALLY DANGEROUS PORTS

For further information on historically dangerous ports, the “Packet Filtering for Firewall Systems” paper available at http://www.cert.org.

# STEALTH SCANS

Stealth ports, by definition, aren’t meant to be detectable. They are based on how the TCP protocol stack responds to unexpected packets, or packets with illegal state flag combinations. For example, an incoming packet that has the ACK flag set but has no related connection. If the ACK were sent to a port with a listening server attached, the TCP stack wouldn’t find a related connection and return a TCP RST message to tell the sender to reset the connection. If the ACK were sent to an unused port, the system would return a TCP RST message as an error indication, as the firewall might return an ICMP error message by default.

The issue is further complicated because some firewalls test only for the SYN flag or the ACK flag. If neither is set, or if the packet contains some combination of flags, the firewall implementation might pass the packet up to the TCP code. Depending on the TCP state flag combination and the operating system receiving the packet, the system will respond with an RST or silence. This mechanism can be used to help identify the operating system that the target system is running. In any of these cases, the receiving system isn’t likely to log the event.

Inducing a target host to generate an RST packet in this manner also be used to map a network, determining the IP addresses of systems listening on the network. This is especially helpful if the target system isn’t a server and its firewall has been set to silently drop unwanted packets.