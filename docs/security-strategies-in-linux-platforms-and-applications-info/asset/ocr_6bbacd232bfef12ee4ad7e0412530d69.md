# PART 2 | Layered Security and Linux

# Printer Administrators

One directive typically located early in the cupsd.conf file is SystemGroup. Groups that are listed after this directive are groups authorized to administer printers in CUPS system. You can add users to the specified group in the /etc/group and /etc/gshadow configuration files. The groups may vary. On Red Hat systems, members of the sys group are default print administrators: on Ubuntu systems, members of the ladmin group are default print administrators.

# Shared Printers

CUPS printers are local, unless remote access is allowed. Remote access starts with the Listen directive, which by default enables access through port 631 on all IP addresses. If you want to limit access to one of multiple network cards on a system, you could set up a directive like the following, where 192.168.0.10 is the IP address of the local network card that is allowed to receive CUPS communications:

```
Listen 192.168.0.10:631
```

If printers are shared through other systems such as Samba, ports for that service must also be open. Shared printers can be shown on the local network with the default directives, which are almost self explanatory. They activate browsing of local printers, and determine whether the BrowseAllow or the BrowseDeny directive is considered first. Either or both of these directives be included with an IP address or domain name for a single host or a network. The final line, the BrowseLocalProtocol specifies the use of printer browsing using CUPS and the DNS-based Service Discovery (DNSSSD) protocol for CUPS print browsing.

Browsing On

+   BrowseOrder allow, deny
BrowseAllow all
BrowseLocalProtocols CUPS dnsssd

# Remote Administration

Remote administration of CUPS servers is based on the three Location stanzas that follow in the cupsd.conf file. The format of the three stanzas is quite similar. They are all confined by Location directives. They all specify host- or possibly user-based access. The difference is based on the label associated with each Location stanza.

The Location stanza supports access to locally configured printers. The default version of this stanza limits such access to the local system:

```
<Location />
Order allow, deny
</Location>
```