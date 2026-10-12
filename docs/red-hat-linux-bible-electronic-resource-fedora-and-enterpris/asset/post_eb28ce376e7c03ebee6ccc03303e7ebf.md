
> **CROSS-REFERENCE:** Information on setting up NetWare services in Red Hat Linux is provided in Chapter 18.

By default, NetWare file and print services are off in Red Hat Linux. To turn them on, type **chkconfig mars_nwe on**. To make the service usable, you must edit `/etc/nwserv.conf`.

## Login servers

A variety of login servers are available for use with Red Hat Linux. Both telnet and login services can be used to allow users from other computers to log in to Red Hat Linux from the network. These days, however, ssh is the preferred login service. For most of these services, you need to remember to allow access to that service from your firewall.

If the telnet-server package is installed, the telnet service is off by default. If telnet is enabled, the xinetd daemon passes all requests for telnet service (by default, port 23) to the in.telnetd daemon to present the telnet login prompt. Once it is on, only users with real logins to the computer can log in to the computer — anonymous users are not supported. Users who log in using telnet are presented with a shell interface for accessing the computer.

Red Hat Linux also includes login daemons that provide Kerberos 5 support. Kerberos 5 provides a higher level of security than is available with other login servers. Kerberos 5-enabled login servers include Klogin (Kerberos 5) and EKlogin (Kerberos 5 with encryption).

The rlogin service has been available for UNIX systems for a long time, though it is generally less secure than the other login services described here. The rlogin service is off by default on your Red Hat Linux system.

A newer addition to the login servers available with Red Hat Linux is the OpenSSH server. This service is on by default. To access this service, use applications that come with the openssh-client software package, such as the ssh, sftp, and slogin remote login commands. Many Linux administrators use OpenSSH tools, as opposed to older remote login tools such as rlogin and telnet because OpenSSH is believed to be more secure.

> **CAUTION:** Not only is the SSH service on by default, but unlike other login services, it will allow root login over the network. If you are uncomfortable with that, you should change the PermitRootLogin yes line in the /etc/ssh/sshd_config file as follows:
> 
> PermitRootLogin no

## E-mail servers

The most common protocols used to download e-mail from a mail server to a client workstation are Post Office Protocol (POP) and Internet Message Protocol (IMAP). If you configure Red Hat Linux as your mail server, you can configure several different POP and IMAP daemons that can allow users to download e-mail to their workstations.

By default, all POP or IMAP services are off. Choose the POP or IMAP server you would like to use from those provided in the e-mail reader servers listing in Table C-1. To turn on that service, simply change the file in /etc/xinetd.d associated with that service so that the disable = yes entry is changed to disable = no. Then restart the xinetd daemon.

The default mail-transfer agent that comes with Red Hat Linux is called sendmail. If sendmail software is installed, the sendmail service is started automatically. However, you must configure various files in the /etc/mail directory for the service to work beyond the localhost.

Postfix is an alternative to sendmail. Using the alternatives feature (described earlier in this appendix and in Ch. 10), you can easily make one or the other your default mail-transfer agent. Configuration files for postfix are located in the /etc/postfix directory. Also make sure that you turn sendmail off (chkconfig sendmail off) and turn postfix on (chkconfig postfix on).

> CROSS-REFERENCE: Chapter 19 contains details on how to configure sendmail and postfix.

The comsat service can be turned on to check when e-mail arrives in users’ mailboxes in Red Hat Linux. Though comsat is off by default, if you turn it on you can use the biff or xbiff commands to alert users when e-mail arrives in their mailboxes. To turn comsat on, simply edit the comsat file in /etc/xinetd.d to change the disable = yes entry to disable = no.

### News server

Red Hat Linux comes with the Internet Network News Server (INN) software to let you set up a Red Hat Linux system as a news server. INN can provide your users access to thousands of Internet newsgroups.

By default, INN service is off in Red Hat Linux. To turn it on, type chkconfig inn on. To make the service usable, you must edit files in the /etc/news directory.

> CAUTION: Because a news server can potentially consume huge amounts of system resources, you must think carefully about how you configure it. See Chapter 22 for details about configuring INN.

### Print servers

The Common UNIX Printing System (CUPS) print server software is included as the default printer software for the current release of Red Hat Linux. As an alternative, the LPR New Generation (LPRng) software is still available but is no longer provided with Red Hat Linux.

> CROSS-REFERENCE: Information on setting up printers can be found in Chapter 17.

The Common UNIX Printing System (CUPS) is a recently developed alternative to LPRng and other printing interfaces that were built on facilities originally designed for line printers in the 1970s. CUPS is based on the Internet Printing Protocol (RFC 2616). Although it is compatible with other UNIX/Linux print facilities, CUPS is intended to make it easier to support new printers, protocols, and other devices as they become available.

The CUPS server (cupsd) is set up to run by default. Because CUPS is configured to be used as the printing service by default, you should run the `redhat-switch-printer` command if you want LPRng as the default print service for your computer. Configuration files for CUPS are located in the /etc/cups directory.

## Network administration servers

Some network servers offer services that monitor or configure network configurations. Several of these services, listed in Table C-1, are described below.

### Network Time Protocol server

The Network Time Protocol (NTP) Server synchronizes time among computers on a network.

The Red Hat Linux firstboot process lets you turn on the ntp service. To further tune ntp, you must edit the /etc/ntp.conf file. The /etc/ntp.conf file contains information that identifies the addresses of synchronization sources and modes of operation. The /etc/ntp/keys file can be used to turn on authentication.

### Portmap server

The portmap server translates Remote Procedure Call (RPC) numbers to TCP/IP and UDP port numbers. Certain network services, such as NFS (nfs) and Wall (rwalld), only work properly if this server is running. RPC numbers are stored in the /etc/rpc file.

### SWAT

The Samba Web Administration Tool (SWAT) provides a Web-based interface for configuring Samba file and print services. Once properly configured, a Web browser can access the SWAT service (with a root user password). Although this is a well-tested interface, the Samba Server Configuration window is the preferred tool for configuring Samba in Red Hat Linux.

By default, the SWAT service is off in Red Hat Linux. To turn the service on, edit the /etc/xinetd.d/swat file and change the `disable = yes` entry to `disable = no`. This makes the service available to a Web browser on the local host that asks for port number 901 (for example, http://localhost:901). You can remove the line `only_from = 127.0.0.1` to allow a Web browser from any computer that has access to your computer on the network to use SWAT. (Of course, a remote user would also need to know your root password.)

### Arpwatch server

The Arpwatch service can be turned on to monitor Ethernet/IP activities on your network. Any potential problems (such as two different computers using the same IP address) are logged to the syslog facility (usually to the `/var/log/messages` file).

By default, the Arpwatch service is turned off. To turn it on, type **chkconfig arpwatch on**. You can check the `/var/log/messages` file to see if the Arpwatch services started successfully and watch for changes on your network.

### Simple Network Management Protocol server

The Simple Network Management Protocol (SNMP) server lets your Red Hat Linux system listen for SNMP requests from the network. With this server running, other computers using SNMP tools can monitor the activities of your computer (based on configuration files set up on your system).

By default, SNMP is turned off. To turn it on, type **chkconfig snmpd on** and **chkconfig snmptrapd on**. SNMP configuration can be quite complex. Start by referring to the *snmpd.conf* man page (type **man snmpd.conf**). Refer to the net-snmp project site (http://net-snmp.sourceforge.net) for a tutorial and other information.

### Information servers

By distributing such information as host names, user account information, and network addresses, an administrator can more easily manage groups of networked computers. Popular types of servers for managing network information include Network Information System (NIS), Dynamic Host Configuration Protocol (DHCP), and Lightweight Directory Access Protocol (LDAP).

### Network Information System servers

Network Information System (NIS) is a software feature developed by Sun Microsystems to manage information needed to configure a group of UNIX (and now Linux) computers on a network. Using NIS, a group of computers can share common **passwd, groups, hosts**, and other configuration files.

By default, NIS services are off. You can turn on NIS services for your Linux computer as either an NIS client (using shared information) or an NIS server (distributing shared information). NIS client computers need to start the `/etc/init.d/ypbind` script and identify the NIS servers in the `/etc/yp.conf` file.

To use Red Hat Linux as an NIS server, you must gather up the configuration files you want to share, then start the `/etc/init.d/ypserv` script. The script runs the `/usr/sbin/ypserv` daemon, which takes care of the distribution of information to the NIS client computers.
