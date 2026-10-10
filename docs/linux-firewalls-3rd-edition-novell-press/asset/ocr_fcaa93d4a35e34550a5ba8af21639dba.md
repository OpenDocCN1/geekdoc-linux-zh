**firewall, screened-host** Almost identical to a dual-homed firewall, the single-host firewall does not sit directly between the Internet and the local network. The screened-host firewall is separated from the public network by an intermediate router and a packet filter. Local users must either specifically connect to the firewall machine to access the Internet or go through proxies on the firewall machine. The screening router ensures that all traffic between networks, or at least specific kinds of traffic, goes through the screened host. The difference between the screened-host firewall and the dual-host firewall is primarily in the location of the firewall within the local network.

**firewall, screened-subnet** A firewall system incorporating a gateway firewall, a DMZ network housing public servers, and an internal choke firewall that screens the LAN from both the DMZ and direct Internet access. Public services are not hosted from the choke firewall.

**flooding, packet** A denial-of-service attack in which the victim host or network is sent more packets of a given type than the victim can accommodate.

**forward** To route packets from one network to another in the process of delivering a packet from one computer to another.

**fragment** An IP packet containing a piece of a TCP segment.

**FTP** File Transfer Protocol. The protocol and programs used to copy files between networked computers.

**FTP, anonymous** FTP service accessible to any client that requests the service.

**FTP, authenticated** FTP service accessible to predefined accounts, which must be authenticated before using the service.

**gateway** A computer or program serving as either the conduit or the termination point and relay between two networks.

**hosts.allow, hosts.deny** TCP wrappers’ configuration files are /etc/hosts.allow and /etc/hosts.deny.

**HOWTO** In addition to the standard man pages, Linux includes user-supplied online documentation on numerous topics, in many languages and in multiple formats. The HOWTO documents are coordinated and maintained by the Linux Documentation Project.

**HTTP** Hypertext Transfer Protocol, used by web servers and browsers.

**hub** A hardware signal repeater used to physically connect multiple network segments, extend the distance of a physical network, or connect network segments of different physical types.

**IANA** Internet Assigned Numbers Authority.