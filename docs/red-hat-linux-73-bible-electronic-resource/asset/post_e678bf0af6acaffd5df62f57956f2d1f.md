
## Login Servers
A newer addition to the login servers available with Red Hat Linux is the OpenSSH server. This service is on by default. To access this service, use applications that come with the openssh-client software package, such as the ssh and slogin remote login commands. Many Linux administrators use OpenSSH tools, as opposed to older remote login tools such as rlogin and telnet because OpenSSH is believed to be more secure.

> **CAUTION**: Not only is the SSH service on by default, but unlike other login services it will allow root login over the network. If you are uncomfortable with that, you should change the `PermitRootLogin yes` line in the `/etc/ssh/sshd_config` file as follows:
> `PermitRootLogin no`

## E-mail Servers
The most common protocols used to download e-mail from a mail server to a client workstation are Post Office Protocol (POP) and Internet Message Protocol (IMAP). If you configure Red Hat Linux as your mail server, you can configure several different POP and IMAP daemons that can allow users to download e-mail to their workstations.

By default, all POP or IMAP services are off. Choose the POP or IMAP server you would like to use from those provided in the e-mail reader servers listing in Table 24-1. To turn on that service, simply change the file in `/etc/xinetd.d` associated with that service so that the `disable = yes` entry is changed to `disable = no`. Then restart the xinetd daemon.

The default mail-transfer agent that comes with Red Hat Linux is called sendmail. If sendmail software is installed, the sendmail service is started automatically. However, you need to configure the `/etc/sendmail.cf` file, as well as several files in `/etc/mail`, for the service to work as you would like it to.

An alternative to sendmail (added to the distribution for Red Hat Linux 7.3) is postfix. Using the alternatives feature (described in the "Choosing Alternatives" section of this appendix), you can safely make one or the other your default mail-transfer agent. Configuration files for postfix are located in the `/etc/postfix` directory. You should also make sure that the start-up file in the directory representing your current run level (probably `/etc/rc3.d` or `/etc/rc5.d`) begins with an S (such as `S80postfix`), and that the sendmail script begins with a K (such as `K30sendmail`).

> **CROSS-REFERENCE**: Chapter 19 contains a detailed description of how to configure sendmail and postfix.

The comsat service can be turned on to check when e-mail arrives in users' mailboxes on your Red Hat Linux system. Though comsat is off by default, if you turn it on, you can use the `biff` or `xbiff` commands to alert users when e-mail arrives in their mailboxes. To turn on comsat, simply change the comsat file in `/etc/xinetd.d` so that the `disable = yes` entry is changed to `disable = no`.

## News Server
Red Hat Linux comes with the Internet News Server (INN) software to let you set up a Red Hat Linux system as a news server. INN can provide your users access to thousands of Internet newsgroups.

By default, INN service is off in Red Hat Linux. To turn it on, change the kill script (`K051nnd`) to a start-up script (`S051nnd`). Do this by changing the files in the directories for run levels in which you want the service to run (probably `/etc/rc3.d` or `/etc/rc5.d`). For the service to be usable, you need to edit files in the `/etc/news` directory.

**CAUTION**: Because a news server can potentially consume huge amounts of system resources, you need to think carefully about how you configure it. See Chapter 22 for details about configuring your INN server.

## Print Servers
The LPR New Generation (LPng) software is included as the default printer software for the current release of Red Hat Linux. As an alternative, the Common UNIX Printing System (CUPS) print server software is available for the first time in this release.

The LPng software is particularly well-suited for organizations in which a lot of people share many printers, such as on college campuses.

The LPng server (`lpd`) is started automatically when you boot your Red Hat Linux system (in run levels 2, 3, 4, or 5). However, unless you add one or more printers to the `/etc/printcap` file, no printers will actually be available for you to share. To add a printer manually, you must edit the `/etc/printcap.local` file. Also, any remote computer that you want to allow to access your computer must be added to the `/etc/lpd.perms` file. Global printing values (that is, ones that apply to all printers) can be added to the `/etc/lpd.conf` file.

**CROSS-REFERENCE**: Information on setting up printers can be found in Chapter 17.

The Common UNIX Printing System (CUPS) is a recently developed alternative to LPng and other printing interfaces that were built on facilities originally designed for line printers in the 1970s. CUPS is based on the Internet Printing Protocol (RFC 2616). Although it is compatible with other UNIX/Linux print facilities, CUPS is intended to make it easier to support new printers, protocols, and other devices as they become available.

The CUPS server (`cupsd`) is set up to run in run levels 2, 3, 4, and 5. However, because LPng is configured to be used as the printing service by default, you should run the `redhat-switch-printer` command if you want CUPS to be the default print service for your computer. Configuration files for CUPS are located in the `/etc/cups` directory.

## Network-Administration Servers
Some network servers offer services that monitor or configure network configurations. Several of these services, listed in Table C-1, are described below.

### Network Time Protocol Server
The Network Time Protocol (NTP) Server synchronizes time among a set of computers on a network.

By default, the NTP service is off in Red Hat Linux. To turn it on, change the `kill` script (`K1ntpd`) to a start-up script (`S10ntpd`). Do this by changing the files in the directories for run levels in which you want the service to run (probably `/etc/rc3.d` or `/etc/rc5.d`). For the service to be usable, you need to edit the `/etc/ntp.conf` file. The `/etc/ntp.conf` file contains information that identifies the addresses of synchronization sources and modes of operation. The `/etc/ntp/keys` file can be used to turn on authentication.

### Portmap Server
The portmap server translates Remote Procedure Call (RPC) numbers to TCP/IP and UDP port numbers. This server must be running in order for certain network services, such as NFS (`nfs`), Rusers (`rusersd`), and Wall (`rwal1d`), to work properly. RPC numbers are stored in the `/etc/rpc` file.

### SWAT
The Samba Web Administration Tool (SWAT) provides a Web-based interface for configuring Samba file and print services. Once properly configured, any Web browser can access the SWAT service (with a root user password).

By default, the SWAT service is off in Red Hat Linux. To turn the service on, edit the `/etc/xinetd.d/swat` file and change the `disable = yes` entry to `disable = no`. This makes the service available to a Web browser on the local host that asks for port number 901 (for example, `http://localhost:901`). You can remove the line `only_from = 127.0.0.1` to allow a Web browser from any computer that has access to your computer on the network to use SWAT. (Of course, someone trying to use the service would also need to know your root password.)

### Arpwatch Server
The Arpwatch service can be turned on to monitor Ethernet/IP activities on your network. Any potential problems (such as two different computers using the same IP address) are logged to the syslog facility (usually to the `/var/log/messages` file).

By default, the Arpwatch service is turned off. To turn it on, change the `kill` script (`K45arpwatch`) to a start-up script (`S45arpwatch`). Do this by changing the files in the directories for run levels in which you want the service to run (probably `/etc/rc3.d` or `/etc/rc5.d`). You can check the `/var/log/messages` file to see if the Arpwatch services started successfully and watch for changes on your network.

### Simple Network Management Protocol (SNMP) Server
The Simple Network Management Protocol (SNMP) server lets your Red Hat Linux system listen for SNMP requests from the network. With this server running, other computers using SNMP tools can monitor (based on configuration files you set up on your system) the activities of your computer.

By default, SNMP is turned off. To turn it on, change the kill script (`K50snmpd`) to a start-up script (`S50snmpd`). Do this by changing the files in the directories for run levels in which you want the service to run (probably `/etc/rc3.d` or `/etc/rc5.d`). SNMP configuration can be quite complex. Start by referring to the `snmpd.conf` man page (type `man snmpd.conf`) and going through the tutorial from the UCD-SNMP home page (`http://ucd-snmp.ucdavis.edu`).

## Information Servers
By distributing such information as host names, user account information, and network addresses, an administrator can more easily manage groups of networked computers. Popular types of servers for managing network information include Network Information System (NIS), Dynamic Host Configuration Protocol (DHCP), and Lightweight Directory Access Protocol (LDAP).

### Network Information System Servers
Network Information System (NIS) is a software feature that was developed by Sun Microsystems to manage information needed to configure a group of UNIX (and now Linux) computers on a network. Using NIS, a group of computers can share common `passwd`, `groups`, `hosts`, and other configuration files.

By default, NIS services are off. You can turn on NIS services for your Linux computer as either an NIS client (using shared information) or an NIS server (distributing shared information). NIS client computers need to start the `/etc/init.d/ypbind` script and identify the NIS servers in the `/etc/yp.conf` file.

If you want to use your Red Hat Linux system as an NIS server, you need to gather up the configuration files you need to share, then start the `/etc/init.d/ypserv` script. The script runs the `/usr/sbin/ypserv` daemon, which takes care of the distribution of information to the NIS client computers.

> **CROSS-REFERENCE**: Chapter 23 describes the NIS client and server software.
