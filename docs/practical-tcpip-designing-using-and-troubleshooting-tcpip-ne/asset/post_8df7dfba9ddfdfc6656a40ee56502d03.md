
# inetd

- □ Linux manpages: inetd(8), inetd.conf(5), services(5)

The program **xinetd** (“*extended inetd*”) is a popular replacement for **inetd**. It offers extensive logging, access control, limits on the number of child processes (to prevent denial-of-service attacks), and many other features. See:

- □ [http://www.xinetd.org/](http://www.xinetd.org/) *xinetd home page*

# FTP

The specification for FTP is

- □ **RFC-959 October 1985** *File Transfer Protocol (FTP)*

The early sections are readable and give some useful background, and its Module 4.2 lists the response codes.

Most publicly accessible FTP servers allow you to logon as user **anonymous** and ask you to give your full e-mail address as password. The username **ftp** is the same as **anonymous** and is much quicker to *type*.

Increasingly HTTP is used instead of FTP for file downloads, but FTP is sometimes used in preference to HTTP because:

- • for the server administrator, it’s easier to just copy a file into an FTP directory than having to build and maintain an HTTP page containing a link to the file. (Some HTTP servers let you list the contents of a directory (below), which diminishes this advantage.)

![](img/a2132b646d336d5f9a21102d6320e537_488_0.png)

- • FTP can do multiple transfers. For example, you can download all PDF files using the FTP command `mget *.pdf` (`mget` means “multiple get”)
- • if an FTP transfer breaks in mid-session, some clients and servers let you restart from where you left off instead of from the beginning of the file again, which is ideal if the files being transferred are very large.

# netcat

- □ [http://freshmeat.net/projects/netcat/](http://freshmeat.net/projects/netcat/)
- □ [http://www.attstake.com/research/tools/index.html](http://www.attstake.com/research/tools/index.html)
- □ [http://www.uit.co.uk/practcp/netcat.pdf](http://www.uit.co.uk/practcp/netcat.pdf) *Netcat tutorial*

# X Window System

For a detailed description of what X is and how it works, see our book:

- Niall Mansfield *The Joy of X - An Overview of the X Window System* (1993, Addison-Wesley)

Good starting points for exploring Linux X resources, Gnome, and KDE are:

- http://www.linuxdoc.org/HOWTO/XWindow-User-HOWTO-11.html
- http://www.kde.org
- http://www.gnome.org
- http://www.linuxdoc.org/LDP/lame/LAME/linux-admin-made-easy/using-gnome.html *GNOME Installation and Configuration*
- http://www.linuxdoc.org/LDP/lame/LAME/linux-admin-made-easy/using-kde.html *KDE Installation and Configuration*
- http://www.gtk.org *The GIMP Toolkit*, which is a multi-platform toolkit for creating graphical interfaces

X now runs on handheld computers:

- http://www.handhelds.org/

and IBM even have it running on a wrist-watch (that runs Linux!).

A related system is VNC ("virtual network computing"):

- http://www.uk.research.att.com/vnc/

which is used widely for remotely managing Microsoft Windows systems. It lets you connect to a Windows system from another Windows system or a Linux/UNIX box running X and display the full screen of the remote system, and use all its capabilities.

# LDAP

- RFC-2251 *December 1997 Lightweight Directory Access Protocol (v3)*

Much of the original work on LDAP was done at the University of Michigan. Their site still has some historical information:

- http://www.umich.edu/~dirsvc/ldap

but this has been superseded by the OpenLDAP project:

- http://www.openldap.org

and some of our examples are from that distribution.

Microsoft's Active Directory:

- http://www.microsoft.com/windows2000/techinfo/howitworks/activedirectory/adarch.asp *Active Directory Architecture*
- http://www.labmice.net/ActiveDirectory/default.htm

Novell’s eDirectory or NDS (Novell Directory Services):

- ☐ http://developer.novell.com/nds/ndsldap.htm

For the DEN (Directory Enabled Network) and other directory initiatives:

- ☐ http://www.dmtf.org/standards/standard_den.php
- ☐ http://www.opengroup.org/directory/ Directory Interoperability Forum. See under “white papers”.

# SNMP

The standard for SNMP is:

- ☐ RFC-1157 May 1990 *A Simple Network Management Protocol*

A lot of work on SNMP has been done at the University of California at Davis (UC Davis). The project page (which used to be at http://ucd-snmp.ucdavis.edu) has been renamed to net-snmp, available at:

- ☐ http://net-snmp.sourceforge.net/

Stevens, Chapter 25 gives a good overview of SNMP. Other good books are hard to find; many books seem to have a small amount of real body text and huge appendices listing MIBs that are better left in machine-readable files. The “SNMP FAQ” available on the net isn’t a good introduction – you have to know what SNMP is about for it to be very useful:

- ☐ ftp://rtfm.mit.edu/pub/usenet/comp.protocols.snmp/comp.protocols.snmp_SNMP_FAQ_Part_1_of_2
- ☐ ftp://rtfm.mit.edu/pub/usenet/comp.protocols.snmp/comp.protocols.snmp_SNMP_FAQ_Part_2_of_2

but the FAQ about the UC Davis tools at http://net-snmp.sourceforge.net/ above is helpful. There’s a great tutorial at:

- ☐ http://www.netcom-sys.com/techdocs.html *SNMP For Dummies*

although it refers quite a bit to the Opitivity network management software from Nortel Networks.

For an explanation of all the SNMP node numbers (all the 1.3.6.2. ... stuff), see:

- ☐ http://www.iana.org/assignments/smi-numbers

and for a listing of the private enterprise numbers, see:

- ☐ http://www.isi.edu/in-notes/iana/assignments/enterprise-numbers

MIB-II is defined in:

- ☐ RFC-1213 March 1991 *Management Information Base for Network Management of TCP/IP-based internets: MIB-II*

MIB modules are written in *ASN.1 (Abstract Syntax Notation 1)* described in:

- ☐ RFC-2578 April 1999 *The Structure of Management Information Version 2 (SMIv2)*

The Windows-NT SNMP tools are included with the NT 4.0 Resource Kit. These include the basic but useful snmpmon tool. This lets you specify a set of SNMP variables on particular hosts, and it monitors them (retrieves their values) periodically; you can execute arbitrary commands depending on the results, e.g. to send an alert or e-mail, or remove temporary files from a directory if the machine is running short of disk space, etc.

Lots of system and network administrators write their own tools from scratch to monitor and control various aspects of their systems (e.g. monitor disk space, check network connections, etc.). Instead of re-inventing the wheel, consider using SNMP instead. It will take you longer initially, but very soon it will save you a lot of time and make your tools more portable and more generally useful.

We haven't covered SNMP traps. Agents have to be pre-configured with the address of the management station – there's no discovery mechanism to enable an SNMP "client" machine to find the management station automatically. (But it can be configured with DHCP.) On NT, snmputil trap listens for traps.

SNMP has only four commands: get and set, which we used, trap, which we discussed above, and finally get-next. get-next returns the value (or OID) of the variable after the one you specified. By specifying the root of the tree, and repeatedly get-nexting, you can retrieve the whole tree, without knowing what's in it or how it's made up. This is one of the features that makes SNMP so powerful. It lets you browse the MIB tree and get any information you're interested in. Linux includes the command snmpwalk, which uses get-next repeatedly to retrieve all the values in the sub-tree below the variable you specify. Below, we show snmpwalk output for the system node. get-next is also essential for handling arrays that you don't know the size of.

```
alice% snmpwalk -On bob public system
1.3.6.1.2.1.1.1.0 = Hardware: x86 Family... Software: Windows NT Version 4.0
1.3.6.1.2.1.1.2.0 = OID: 1.3.6.1.4.1.311.1.1.3.1.3
1.3.6.1.2.1.1.3.0 = Timeticks: (663334843) 76 days, 18:35:48.43
1.3.6.1.2.1.1.4.0 =
1.3.6.1.2.1.1.5.0 = BOB
1.3.6.1.2.1.1.6.0 = Server rack no. 4
1.3.6.1.2.1.1.7.0 = 76
alice%
```

There's a good graphical SNMP tool for Microsoft Windows called getif ("get interface information") available from:

- □ http://www.wtcs.org/snmp4tcp/

# Syslog

Even though Syslog is very old, it has only recently been documented as an RFC:

- □ RFC-3164 August 2001 The BSD Syslog Protocol

which gives a lot of readable background. syslog and similar services can be critical in logging and monitoring systems, but Syslog over UDP doesn't give the sender any feedback on whether the message has been logged successfully. A recent RFC specifies how syslog can be run over a reliable (TCP) connection, and with enhanced data integrity and security:

- □ RFC-3195 November 2001 Reliable Delivery for Syslog
