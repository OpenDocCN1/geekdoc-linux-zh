
# Netalk server

The Netalk server software lets Linux act as an AppleTalk server for Macintosh computers. To use netalk, you must install the netalk package and turn on the service by typing **chkconfig atalk on**. Configuration is done from files in the `/etc/atalc` directory.

**CROSS-REFERENCE: See Chapter 26 for information on setting up netalk.**

# NetWare server

NetWare is an operating system from Novell, Inc. that provides dedicated file and print services to network users. The mars-nwe package lets you set up your computer to emulate a NetWare file server. Although mars-nwe is no longer distributed with Fedora Linux, the package is available from various software repositories.

If you install mars-nwe, by default, NetWare file and print services are off. To turn them on, type **chkconfig mars_nwe on**. To make the service usable, you must edit the `/etc/nwserv.conf` file.

# Login servers

A variety of login servers are available for use with Fedora Linux. Both telnet and rlogin services can be used to allow users from other computers to log in to Fedora Linux from the network. These days, however, *ssh* is the preferred login service. For most of these services, you need to remember to allow access to that service from your firewall.

If the telnet-server package is installed, the telnet service is off by default. If telnet is enabled, the *xinetd* daemon passes all requests for telnet service (by default, port 23) to the *in.telnetd* daemon to present the telnet login prompt. Once it is on, only users with real logins to the computer can log in to the computer — anonymous users are not supported. Users who log in using telnet are presented with a shell interface for accessing the computer.

Fedora Linux also includes login daemons that provide Kerberos 5 support. Kerberos 5 provides a higher level of security than is available with other login servers. Kerberos 5-enabled login servers include Klogin (Kerberos 5) and EKlogin (Kerberos 5 with encryption).

The *rlogin* service has been available for UNIX systems for a long time, though it is generally less secure than the other login services described here. The *rlogin* service is off by default on your Fedora Linux system.

A newer addition to the login servers available with Fedora Linux is the OpenSSH server. This service is on by default. To access this service, use applications that come with the *openssh-client* software package, such as the *ssh*, *sftp*, and *slogin* remote login commands. Many Linux administrators use OpenSSH tools, as opposed to older remote login tools such as *rlogin* and *telnet* because OpenSSH is believed to be more secure.

**CAUTION:** Not only is the SSH service on by default, but unlike other login services, it will allow root login over the network. If you are uncomfortable with that, you should change the `PermitRootLogin` line in the `/etc/ssh/sshd_config` file as follows:

`PermitRootLogin` no

# E-mail servers

The most common protocols used to download e-mail from a mail server to a client workstation are Post Office Protocol (POP) and Internet Message Protocol (IMAP). If you configure Fedora Linux as your mail server, you can configure the dovecot package to provide POP and IMAP services.

Dovecot is an IMAP/POP3 mail server that works with both maildir and mbox formats. You use IMAP or POP3 if your users get their mail from their own desktop instead of by running their mail clients on the mail server. By default, all POP or IMAP services are off. Choose the POP or IMAP server you would like to use from those provided in the e-mail reader servers listing in Table C-1.

The default mail-transfer agent that comes with Fedora Linux is called sendmail. If sendmail software is installed, the sendmail service is started automatically. However, you must configure various files in the `/etc/mail` directory for the service to work beyond the localhost.

Postfix is an alternative to sendmail, as is the exim mail transport agent. Using the alternatives feature (described earlier in this appendix and in Chapter 10), you can easily make any of those packages your default mail-transfer agent. Configuration files for Postfix are located in the `/etc/postfix` directory, while exim configuration files are in the `/etc/exim` directory. Also make sure that you turn sendmail off (`chkconfig sendmail off`) and turn postfix or exim on (`chkconfig postfix on` or `chkconfig exim on`).

**CROSS-REFERENCE:** Chapter 19 contains details on how to configure sendmail and postfix.

The comsat service can be turned on to check when e-mail arrives in users’ mailboxes in Fedora Linux. Though comsat is off by default, if you turn it on you can use the `biff` or `xbiff` commands to alert users when e-mail arrives in their mailboxes. To turn comsat on, simply edit the comsat file in `/etc/xinetd.d` to change the `disable = yes` entry to `disable = no`.

# News server

Fedora Linux comes with the Internet Network News Server (INN) software to let you set up a Fedora Linux system as a news server. INN can provide your users access to thousands of Internet newsgroups.

By default, INN service is off in Fedora Linux. To turn it on, type **chkconfig inn on**. To make the service usable, you must edit files in the /etc/news directory.

> **CAUTION:** Because a news server can potentially consume huge amounts of system resources, you must think carefully about how you configure it. Details about how to configure an INN news server are available from the Red Hat Fedora Linux 3 Bible Web site: www.wiley.com/go/fedora3bible.

# Print servers

The Common UNIX Printing System (CUPS) print server software is included as the default printer software for the current release of Fedora Linux. As an alternative, the LPR New Generation (LPRng) software is still available but is no longer provided by Fedora Linux.

> **CROSS-REFERENCE:** Information on setting up printers can be found in Chapter 17.

The Common UNIX Printing System (CUPS) is a recently developed alternative to LPRng and other printing interfaces that were built on facilities originally designed for line printers in the 1970s. CUPS is based on the Internet Printing Protocol (RFC 2616). Although it is compatible with other UNIX/Linux print facilities, CUPS is intended to make it easier to support new printers, protocols, and other devices as they become available.

The CUPS server (cupsd) is set up to run by default. Configuration files for CUPS are located in the /etc/cups directory.

# Network administration servers

Some network servers offer services that monitor or configure network configurations. Several of these services, listed in Table C-1, are described in the following sections.

## Network Time Protocol server

The Network Time Protocol (NTP) Server synchronizes time among computers on a network.

The Fedora Linux firstboot process lets you turn on the NTP service. To further tune ntp, you must edit the /etc/ntp.conf file. The /etc/ntp.conf file contains information that identifies the addresses of synchronization sources and modes of operation. The /etc/ntp/keys file can be used to turn on authentication.

## Portmap server

The portmap server translates Remote Procedure Call (RPC) numbers to TCP/IP and UDP port numbers. Certain network services, such as NFS (nfs) and Wall (rwalld), only work properly if this server is running. RPC numbers are stored in the /etc/rpc file.

## SWAT

The Samba Web Administration Tool (SWAT) provides a Web-based interface for configuring Samba file and print services. When properly configured, a Web browser can access the SWAT service (with a root user password). Although this is a well-tested interface, the Samba Server Configuration window is the preferred tool for configuring Samba in Fedora Linux.

By default, the SWAT service is off in Fedora Linux. To turn the service on, edit the /etc/xinetd.d/swat file and change the disable = yes entry to disable = no. This makes the service available to a Web browser on the local host that asks for port number 901 (for example, http://localhost:901). You can remove the line only_from = 127.0.0.1 to allow a Web browser from any computer that has access to your computer on the network to use SWAT. (Of course, a remote user would also need to know your root password.)

## Arpwatch server

The Arpwatch service can be turned on to monitor Ethernet/IP activities on your network. Any potential problems (such as two different computers using the same IP address) are logged to the syslog facility (usually to the /var/log/messages file).

By default, the Arpwatch service is turned off. To turn it on, type chkconfig arpwatch on. You can check the /var/log/messages file to see if the Arpwatch services started successfully and watch for changes on your network.

## Simple Network Management Protocol server

The Simple Network Management Protocol (SNMP) server lets your Fedora Linux system listen for SNMP requests from the network. With this server running, other computers using SNMP tools can monitor the activities of your computer (based on configuration files set up on your system).

By default, SNMP is turned off. To turn it on, type chkconfig snmpd on and chkconfig snmptrapd on. SNMP configuration can be quite complex. Start by referring to the snmpd.conf man page (type man snmpd.conf). Pay special attention to security issues with SNMP. Refer to the net-snmp project site (http://net-snmp.sourceforge.net) for a tutorial and more information.

# Information servers

By distributing such information as host names, user account information, and network addresses, an administrator can more easily manage groups of networked computers. Popular types of servers for managing network information include Network Information System (NIS), Dynamic Host Configuration Protocol (DHCP), and Lightweight Directory Access Protocol (LDAP).
