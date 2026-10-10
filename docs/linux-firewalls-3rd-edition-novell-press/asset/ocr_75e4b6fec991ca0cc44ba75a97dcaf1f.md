network and apply completely different packet filtering and access policies to those machines. If services are offered from internal machines, is this fact visible to the outside, or are the services proxied or transparently forwarded via NAT so that they appear to be available from the firewall machine?

How much information do you want to make publicly available about the machines on your LAN? Do you intend to host local DNS services? Are local DNS database contents available to the Internet?

Can people log in to your machines from the Internet? How many and which local machines are accessible to them? Do all user accounts have the same access rights? Will incoming connections be proxied for additional access control?

Are all internal machines equally accessible to local users and from all local machines? Are external services equally accessible from all internal machines? For example, if you use a screened-host firewall architecture, users must log in to the firewall machine directly to have access to the Internet. No routing would be done at all.

Are private LAN services running behind the firewall? For example, is NFS used internally, or do you use NIS, or Samba, or a networked printer, or the Berkeley remote commands, such as rsh, rlogin, and rcp? Do you need to keep any of these services from leaking information or broadcast traffic to the Internet, such as SNMP, DHCP, timed, ntpd, ruptime, or rwho? Maintaining such services behind the secondary choke firewall ensures complete isolation of these services from the Internet.

Related to services designed for LAN use are questions about local versus external access to services designed for Internet use. Will you offer FTP internally but not externally, or will you possibly offer different kinds of FTP services to both? Will you run a private web server or configure different parts of the same site to be available to local users as opposed to remote users? Will you run a local mail server to send mail but use a different mechanism to retrieve incoming mail from the Internet (that is, will you mail be delivered directly to your machine's user accounts, or will you explicitly retrieve mail from an ISP?)

# Configuration Options for a Trusted Home LAN

You must consider two kinds of internal network traffic. The first kind is local access to the gateway firewall, through the internal interface, as shown in Figure 6.4. The second is local access to the Internet, through the gateway machines' external interface.