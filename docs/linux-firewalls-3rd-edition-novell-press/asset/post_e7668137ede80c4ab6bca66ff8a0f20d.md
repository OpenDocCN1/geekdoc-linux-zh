
## DMZ: A Perimeter Network by Any Other Name

  A perimeter network between two firewalls is called a demilitarized zone (DMZ). The purpose of a DMZ is to establish a protected space from which to run public servers (or services) and to isolate that space from the rest of the private LAN. If a server in the DMZ is compromised, that server remains isolated from the LAN; the gateway firewalls and bastion firewalls running on the other DMZ servers offer protection against the compromised server.

  In addition to the single-system, standalone firewall, the firewall presented in Chapter 4 can be expanded to form the basis for a dual-homed gateway firewall protecting the host, which offers one or a few public services. A home LAN is often protected by a single gateway firewall that both filters forwarded traffic and offers public services.

  What options are available for a dual-homed system that can’t afford the risk of a single gateway firewall or the cost of many computers and a staff to manage them? Fortunately, a dual-homed firewall and LAN offer stronger security when the system is configured carefully. The question is this: Is the extra effort worth the increased security in a trusted environment?

### Basic Gateway Firewall Setups

  Two basic gateway firewall setups are used here. As shown in Figure 6.1, the gateway has two network interfaces: one connected to the Internet and one connected to the DMZ. Public Internet services are offered from machines in the DMZ network. The gateway firewall offers no services. A second firewall, a choke firewall, is also connected to the DMZ network, separating the internal, private networks from the quasi-public server machines in the perimeter network. Private machines are protected behind the choke firewall on the internal LAN. Additionally, each of the server machines in the DMZ runs a specialized firewall of its own. If the gateway firewall or one of the servers fails, the public server machines in the DMZ continue to run their individual firewalls. The choke firewall protects the internal LAN from a compromised gateway or from any other compromised machine in the perimeter network. Traffic between the LAN and the Internet passes through both firewalls and crosses the perimeter network.

  In the second setup, the gateway has three network interfaces: one connected to the Internet, one connected to the DMZ, and one connected to the private LAN. As shown in Figure 6.2, traffic between the LAN and the Internet, and traffic between the DMZ and the Internet, share nothing except the gateway’s external network interface.

  **FIGURE 6.1**
  A DMZ between a dual-homed gateway and a choke firewall.
  
  ![](img/d1359a287d9d43cd5ed19f3a7b55d40d_235_0.png)

  **FIGURE 6.2**
  A tri-homed firewall separating a LAN and a DMZ.
  
  ![](img/d1359a287d9d43cd5ed19f3a7b55d40d_235_1.png)

  An advantage of this configuration over the first is that neither the LAN nor the DMZ shares the traffic load of both networks. Another advantage is that it's easier to define rules that refer to all LAN or DMZ traffic specifically, as opposed to traffic related to the other network. Another advantage is that a single-gateway host is less expensive than two separate firewall devices.

  The disadvantage of this configuration over the first is that the gateway becomes a single point of failure for both networks. Also, the firewall rules in the single host include all the complexity related to both the DMZ and the LAN. This complexity can become a confusing issue when you're developing firewall rules by hand.

  A common third alternative is to add a filtering router that separates LAN and DMZ traffic. DMZ servers run their own bastion firewalls. There may or may not be a generalized firewall between the router and the DMZ. As shown in Figure 6.3, the gateway firewall is separate from the router and protects the LAN. The filtering router performs some of the basic filtering for both the LAN and the DMZ. The gateway firewall doesn't need to provide this basic filtering, and it effectively functions similarly to the choke firewall in the first setup.

  **FIGURE 6.3**
  A filtering router in front of LAN and DMZ firewalls.
  
  ![](img/d1359a287d9d43cd5ed19f3a7b55d40d_236_0.png)

## LAN Security Issues

  Security issues are largely dependent on the size of the LAN, its architecture, and what it's used for. The services and architecture are also influenced by the public IP addressing available to the site. Perhaps even more basic than that is the type of Internet connection the site has: dial-up, DSL, wireless, cable, satellite, ISDN, leased line, or any of the other types of Internet connections. Following are some questions you should consider when creating a security policy for your site.

  - Is a public IP address dynamically and temporarily assigned via DHCP or IPCP? Does the site have a single permanently assigned public IP address or a block of them?
  - Are services offered to the Internet? Are these services hosted on the firewall machine, or are they hosted on internal machines? For example, you might offer email service from the gateway firewall machine but serve a website from an internal machine in the DMZ. When services are hosted from internal machines, you want to place those machines on a perimeter network and apply completely different packet filtering and access policies to those machines. If services are offered from internal machines, is this fact visible to the outside, or are the services proxied or transparently forwarded via NAT so that they appear to be available from the firewall machine?
  - How much information do you want to make publicly available about the machines on your LAN? Do you intend to host local DNS services? Are local DNS database contents available to the Internet?
  - Can people log in to your machines from the Internet? How many and which local machines are accessible to them? Do all user accounts have the same access rights? Will incoming connections be proxied for additional access control?
  - Are all internal machines equally accessible to local users and from all local machines? Are external services equally accessible from all internal machines? For example, if you use a screened-host firewall architecture, users must log in to the firewall machine directly to have access to the Internet. No routing would be done at all.
  - Are private LAN services running behind the firewall? For example, is NFS used internally, or do you use NIS, or Samba, or a networked printer, or the Berkeley remote commands, such as rsh, rlogin, and rcp? Do you need to keep any of these services from leaking information or broadcast traffic to the Internet, such as SNMP, DHCP, timed, ntpd, ruptime, or rwho? Maintaining such services behind the secondary choke firewall ensures complete isolation of these services from the Internet.
  - Related to services designed for LAN use are questions about local versus external access to services designed for Internet use. Will you offer FTP internally but not externally, or will you possibly offer different kinds of FTP services to both? Will you run a private web server or configure different parts of the same site to be available to local users as opposed to remote users? Will you run a local mail server to send mail but use a different mechanism to retrieve incoming mail from the Internet (that is, will mail be delivered directly to your machine's user accounts, or will you explicitly retrieve mail from an ISP?)

## Configuration Options for a Trusted Home LAN

  You must consider two kinds of internal network traffic. The first kind is local access to the gateway firewall, through the internal interface, as shown in Figure 6.4. The second is local access to the Internet, through the gateway machines' external interface.

  **FIGURE 6.4**
  LAN traffic to the firewall machine and to the Internet.
  
  ![](img/d1359a287d9d43cd5ed19f3a7b55d40d_238_0.png)

  Presumably, most small systems have no reason to filter packets between the firewall and the local network in general. However, because most home-based sites are assigned a single IP address, one exception arises: NAT. Presumably, the only internal filtering-related action you must take will be to enable your own form of source address spoofing by applying NAT packets moving between your internal machines and the Internet. Most of the emphasis is on filtering packets between the firewall and the Internet.

  > Although small-business and residential sites often like to view their networks as “trusted,” this is often not the case. The problem isn't the local users, but rather the high incidence rate of compromise among these systems. For more information, see CERT Advisory CA-2001-20, “Continuing Threats to Home Users,” at http://www.cert.org/advisories/CA-2001-20.html. For additional information on networking in general, and security in particular, see CERT’s informational paper, “Home Network Security,” at http://www.cert.org/tech_tips/home_networks.html.
