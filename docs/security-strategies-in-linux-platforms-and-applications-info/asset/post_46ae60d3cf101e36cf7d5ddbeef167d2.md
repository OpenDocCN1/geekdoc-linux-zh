
# CHAPTER 9 | Networked Application Security

- Virtual LANs (VLANs)—The network partitions enabled by virtual LANs (VLANs) can keep traffic separate.

- Appropriate firewall rules—Voice traffic requires some priority; firewall rules should be set with a type of service (TOS) that minimizes delay with a switch such as -j TOS --set Minimize-Delay.

- Limit packet floods—Firewall rules allow connections over the SIP and RTP protocols but should stop SYN flood attacks.

## Asterisk Authentication

Without authentication, black-hat hackers may be able to hijack a call on either end of the connection. Asterisk authentication is possible by a number of methods, including the Lightweight Directory Access Protocol (LDAP), the Remote Authentication Dial In User Service (RADIUS), and host-based authentication.

## More Asterisk Security Options

Additional Asterisk security options use information at the data link layer of the TCP/IP protocol suite. These security options include the following:

- Dynamic Host Configuration Protocol (DHCP) snooping—DHCP snooping limits network access to systems with known IP and hardware addresses.

- Dynamic address resolution (ARP) inspection—This checks the binding between the IP address and Media Access Control (MAC) hardware addresses, minimizing the risk of spoofed hardware addresses.

- IP Source Guard—Checks IP addresses against associated hardware addresses based on information stored in a DHCP lease file.

- VLAN access control lists (ACLs)—Reviews ACLs created for a VLAN to minimize the risk of spoofing.

## Limit Printers

The standard service for Linux printer configuration and management is the Common UNIX Printing System (CUPS). It is a versatile system. When the default version of CUPS communicates with the Internet Protocol (IPP) on port 631, it can be used to manage printers from a variety of other services, including Samba, the older Line Printer next generation (LPring), HP JetDirect printers, and more. Microsoft operating supports IPP. Apple owns CUPS software and has maintained it under open source licenses. Because the Macintosh operating system is based on a relative of Linux, the Berkeley Distribution, has made CUPS the default print server for its operating systems.

CUPS is configured in files in the /etc/cups/ directory. The main CUPS configuration file is cups.conf, the focus of this section.

# PART 2 | Layered Security and Linux

## Printer Administrators

One directive typically located early in the cupsd.conf file is SystemGroup. Groups that are listed after this directive are groups authorized to administer printers in CUPS system. You can add users to the specified group in the /etc/group and /etc/gshadow configuration files. The groups may vary. On Red Hat systems, members of the sys group are default print administrators: on Ubuntu systems, members of the ladmin group are default print administrators.

## Shared Printers

CUPS printers are local, unless remote access is allowed. Remote access starts with the Listen directive, which by default enables access through port 631 on all IP addresses. If you want to limit access to one of multiple network cards on a system, you could set up a directive like the following, where 192.168.0.10 is the IP address of the local network card that is allowed to receive CUPS communications:

```
Listen 192.168.0.10:631
```

If printers are shared through other systems such as Samba, ports for that service must also be open. Shared printers can be shown on the local network with the default directives, which are almost self-explanatory. They activate browsing of local printers, and determine whether the BrowseAllow or the BrowseDeny directive is considered first. Either or both of these directives be included with an IP address or domain name for a single host or a network. The final line, the BrowseLocalProtocol specifies the use of printer browsing using CUPS and the DNS-based Service Discovery (DNSSSD) protocol for CUPS print browsing.

### Browsing On

- BrowseOrder allow, deny
BrowseAllow all
BrowseLocalProtocols CUPS dnsssd

## Remote Administration

Remote administration of CUPS servers is based on the three Location stanzas that follow in the cupsd.conf file. The format of the three stanzas is quite similar. They are all confined by Location directives. They all specify host- or possibly user-based access. The difference is based on the label associated with each Location stanza.

The Location stanza supports access to locally configured printers. The default version of this stanza limits such access to the local system:

```
<Location />
Order allow, deny
</Location>
```

You can extend access to the local network with the following directive:

```
Allow @LOCAL
```

If desired, you can substitute an IP address and network mask for the target network, such as from 192.168.0.0/255.255.255.0. Systems on the noted network might also have access to administrative tools and configuration files, depending on the stanzas that follow. Alternatively, you could limit access even further with a couple of directives such as the following:

```
Allow from 192.168.0.10
Deny from 192.168.0.0/255.255.255.0
```

The second stanza, with the <Location /admin> directive, allows access to administrative areas, to allow a review of current print settings.

The third stanza defines users and systems to add and modify printers on the local CUPS service. The AuthType directive refers to the regular user-authentication database. Require user @system points to the SystemGroup directive. Because the @system points to the SystemGroup directive.

```
<Location /admin>
AuthType regular
Require user @system
Order allow, deny
</Location>
```

### The @system directive

The @system directive refers to the SystemGroup defined in the cupsd.conf file. Because the @system points to the SystemGroup directive, it allows you to specify a group of users rather than individual accounts.

### The Location stanza

The Location stanza supports access to locally configured printers. The default version of this stanza limits such access to the local system:

```
<Location />
Order allow, deny
</Location>
```

You can extend access to the local network with the following directive:

```
Allow @LOCAL
```

If desired, you can substitute an IP address and network mask for the target network, such as from 192.168.0.0/255.255.255.0. Systems on the noted network might also have access to administrative tools and configuration files, depending on the stanzas that follow. Alternatively, you could limit access even further with a couple of directives such as the following:

```
Allow from 192.168.0.10
Deny from 192.168.0.0/255.255.255.0
```

The second stanza, with the <Location /admin> directive, allows access to administrative areas, to allow a review of current print settings.

The third stanza defines users and systems to add and modify printers on the local CUPS service. The AuthType directive refers to the regular user-authentication database. Require user @system points to the SystemGroup directive.

```
<Location /admin>
AuthType regular
Require user @system
Order allow, deny
</Location>
```

### The Administrative Tool

The @system directive refers to the SystemGroup defined in the cupsd.conf file. Because the @system points to the SystemGroup directive, it allows you to specify a group of users rather than individual accounts.

### The Location stanza

The Location stanza supports access to locally configured printers. The default version of this stanza limits such access to the local system:

```
<Location />
Order allow, deny
</Location>
```

You can extend access to the local network with the following directive:

```
Allow @LOCAL
```

If desired, you can substitute an IP address and network mask for the target network, such as from 192.168.0.0/255.255.255.0. Systems on the noted network might also have access to administrative tools and configuration files, depending on the stanzas that follow. Alternatively, you could limit access even further with a couple of directives such as the following:

```
Allow from 192.168.0.10
Deny from 192.168.0.0/255.255.255.0
```

The second stanza, with the <Location /admin> directive, allows access to administrative areas, to allow a review of current print settings.

The third stanza defines users and systems to add and modify printers on the local CUPS service. The AuthType directive refers to the regular user-authentication database. Require user @system points to the SystemGroup directive.

```
<Location /admin>
AuthType regular
Require user @system
Order allow, deny
</Location>
```

### The @system directive

The @system directive refers to the SystemGroup defined in the cupsd.conf file. Because the @system points to the SystemGroup directive, it allows you to specify a group of users rather than individual accounts.

### The Location stanza

The Location stanza supports access to locally configured printers. The default version of this stanza limits such access to the local system:

```
<Location />
Order allow, deny
</Location>
```

You can extend access to the local network with the following directive:

```
Allow @LOCAL
```

If desired, you can substitute an IP address and network mask for the target network, such as from 192.168.0.0/255.255.255.0. Systems on the noted network might also have access to administrative tools and configuration files, depending on the stanzas that follow. Alternatively, you could limit access even further with a couple of directives such as the following:

```
Allow from 192.168.0.10
Deny from 192.168.0.0/255.255.255.0
```

The second stanza, with the <Location /admin> directive, allows access to administrative areas, to allow a review of current print settings.

The third stanza defines users and systems to add and modify printers on the local CUPS service. The AuthType directive refers to the regular user-authentication database. Require user @system points to the SystemGroup directive.

## Protect Your Time Services

Time services on Linux rely on NTP. Basic information on NTP configuration was covered in Chapter 8. This section goes further, describing those directives in /etc/ntp.conf that can secure a local NTP server. If an NTP server is overloaded by any, it may not be a security issue per se. However, it affects the reliability of time. For example, if the NTP server is not synchronized to, customers may try to order products that are out of stock.

The security-related directive in this file is restrict. Take a look at the directive as configured in the default ntp.conf. The -4 and -6 correspond to IPv4 and IPv6

```
restrict -4 default kod notrap notify nopeer noquery
restrict -6 kod notrap notify nopeer noquery
```

The other options affect security in the following ways:
- default—Access to all clients is allowed by default.
- kod—Prevents attacks from kiss of death (KOD) packets.
- notrap—Prevents access to the trap service for logging.
- modify—Prevents other NTP servers from modifying the status of this server.
- nopeer—Disallows attachments from other NTP servers.
- noquery—Disallows queries of the NTP service.

Assuming you don't want to open this up as a public NTP server, the default option should not be used. However, some address is required; one option is the IP address of the local network. In addition, you may want to allow time queries, and allow other NTP servers, perhaps from remote networks administered by colleagues, to communicate with your NTP server. The IPv4 restrict directive would change to the following:

```
restrict -4 192.168.0.0 mask 255.255.255.0 kod notrap modify
```

In a similar fashion, you could set up restrictions on the IPv6 network:

```
restrict -6 0011:838:0:1:: mask fffff:ffff:ffff:
kod notrap modify
```

![img/c060a8c8a077903dfec4ff61ffa1302.png]

## Options for Obscurity: Different Ports, Alternative Services

To some extent, when you installed Linux, you made a choice for obscurity. But as you've seen so far in this book, obscurity can mean different things when applied to different services. Obscurity goes beyond the use of nonstandard ports for network communications.
